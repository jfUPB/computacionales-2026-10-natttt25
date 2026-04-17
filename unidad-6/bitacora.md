# Unidad 6

## Bitácora de proceso de aprendizaje
ofApp.h:

	#pragma once
	
	#include "ofMain.h"
	#include <string>
	#include <vector>
	
	class Observer {
	public:
	    virtual ~Observer() = default;
	    virtual void onNotify(const std::string & event) = 0;
	};
	
	class Subject {
	public:
	    void addObserver(Observer * observer);
	    void removeObserver(Observer * observer);
	
	protected:
	    void notify(const std::string & event);
	
	private:
	    std::vector<Observer *> observers;
	};
	
	class Particle;
	
	class State {
	public:
	    virtual ~State() = default;
	    virtual void update(Particle * particle) = 0;
	    virtual void onEnter(Particle * particle) { }
	    virtual void onExit(Particle * particle) { }
	};
	
	class Particle : public Observer {
	public:
	    Particle();
	    ~Particle() override;
	
	    Particle(const Particle &) = delete;
	    Particle & operator=(const Particle &) = delete;
	
	    void update();
	    void draw();
	    void onNotify(const std::string & event) override;
	
	    void setState(State * newState);
	
	    ofVec2f position;
	    ofVec2f velocity;
	    float size;
	    ofColor color;
	
	private:
	    void keepInsideWindow();
	    State * state;
	};
	
	class NormalState : public State {
	public:
	    void update(Particle * particle) override;
	    void onEnter(Particle * particle) override;
	};
	
	class AttractState : public State {
	public:
	    void update(Particle * particle) override;
	};
	
	class RepelState : public State {
	public:
	    void update(Particle * particle) override;
	};
	
	class StopState : public State {
	public:
	    void update(Particle * particle) override;
	};
	
	// NUEVO ESTADO
	class WaveState : public State {
	public:
	    void update(Particle * particle) override;
	    void onEnter(Particle * particle) override;
	};
	
	class ParticleFactory {
	public:
	    static Particle * createParticle(const std::string & type);
	};
	
	class ofApp : public ofBaseApp, public Subject {
	public:
	    ~ofApp() override;
	    void setup() override;
	    void update() override;
	    void draw() override;
	    void keyPressed(int key) override;
	
	private:
	    std::vector<Particle *> particles;
	};


ofApp.cpp
	
	#include "ofApp.h"
	#include <algorithm>
	
	void Subject::addObserver(Observer * observer) {
	    if (!observer) return;
	    if (std::find(observers.begin(), observers.end(), observer) == observers.end()) {
	        observers.push_back(observer);
	    }
	}
	
	void Subject::removeObserver(Observer * observer) {
	    if (!observer) return;
	    observers.erase(std::remove(observers.begin(), observers.end(), observer), observers.end());
	}
	
	void Subject::notify(const std::string & event) {
	    for (Observer * observer : observers) {
	        observer->onNotify(event);
	    }
	}
	
	Particle::Particle()
	    : state(nullptr) {
	    position = ofVec2f(ofRandomWidth(), ofRandomHeight());
	    velocity = ofVec2f(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	    size = ofRandom(2.0f, 5.0f);
	    color = ofColor(255);
	
	    state = new NormalState();
	    state->onEnter(this);
	}
	
	Particle::~Particle() {
	    if (state) {
	        state->onExit(this);
	        delete state;
	        state = nullptr;
	    }
	}
	
	void Particle::setState(State * newState) {
	    if (state) {
	        state->onExit(this);
	        delete state;
	    }
	    state = newState;
	    if (state) {
	        state->onEnter(this);
	    }
	}
	
	void Particle::update() {
	    if (state) {
	        state->update(this);
	    }
	    keepInsideWindow();
	}
	
	void Particle::draw() {
	    ofPushStyle();
	    ofSetColor(color);
	    ofDrawCircle(position, size);
	    ofPopStyle();
	}
	
	void Particle::onNotify(const std::string & event) {
	    if (event == "attract") {
	        setState(new AttractState());
	    } else if (event == "repel") {
	        setState(new RepelState());
	    } else if (event == "stop") {
	        setState(new StopState());
	    } else if (event == "normal") {
	        setState(new NormalState());
	    }
	    // 🔵 NUEVO EVENTO
	    else if (event == "wave") {
	        setState(new WaveState());
	    }
	}
	
	void Particle::keepInsideWindow() {
	    const float W = static_cast<float>(ofGetWidth());
	    const float H = static_cast<float>(ofGetHeight());
	
	    if (position.x < 0.0f) { position.x = 0.0f; velocity.x *= -1.0f; }
	    else if (position.x > W) { position.x = W; velocity.x *= -1.0f; }
	    if (position.y < 0.0f) { position.y = 0.0f; velocity.y *= -1.0f; }
	    else if (position.y > H) { position.y = H; velocity.y *= -1.0f; }
	}
	
	void NormalState::onEnter(Particle * particle) {
	    particle->velocity.set(ofRandom(-0.5f, 0.5f), ofRandom(-0.5f, 0.5f));
	}
	
	void NormalState::update(Particle * particle) {
	    particle->position += particle->velocity;
	}
	
	static void steer(Particle * particle, const ofVec2f & toward, float accel, float vmax, float posScale) {
	    ofVec2f dir = toward - particle->position;
	    float len = dir.length();
	    if (len > 1e-6f) { dir /= len; particle->velocity += dir * accel; }
	    particle->velocity.limit(vmax);
	    particle->position += particle->velocity * posScale;
	}
	
	void AttractState::update(Particle * particle) {
	    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	    steer(particle, mouse, 0.05f, 3.0f, 0.2f);
	}
	
	void RepelState::update(Particle * particle) {
	    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
	    ofVec2f away = particle->position - mouse;
	    float len = away.length();
	    if (len > 1e-6f) { away /= len; particle->velocity += away * 0.05f; }
	    particle->velocity.limit(3.0f);
	    particle->position += particle->velocity * 0.2f;
	}
	
	void StopState::update(Particle * particle) {
	    particle->velocity *= 0.80f;
	    if (particle->velocity.lengthSquared() < 1e-4f) { particle->velocity.set(0.0f, 0.0f); }
	    particle->position += particle->velocity;
	}
	
	// 🔵 NUEVO ESTADO
	void WaveState::onEnter(Particle * particle) {
	    particle->color = ofColor(255, 255, 0);
	}
	
	void WaveState::update(Particle * particle) {
	    float t = ofGetElapsedTimef();
	    particle->position.x += sin(t + particle->position.y * 0.01f) * 2.0f;
	    particle->position.y += particle->velocity.y;
	}
	
	Particle * ParticleFactory::createParticle(const std::string & type) {
	    Particle * particle = new Particle();
	    if (type == "star") {
	        particle->size = ofRandom(2.0f, 4.0f);
	        particle->color = ofColor(255, 0, 0);
	    } else if (type == "shooting_star") {
	        particle->size = ofRandom(3.0f, 6.0f);
	        particle->color = ofColor(0, 255, 0);
	        particle->velocity *= 3.0f;
	    } else if (type == "planet") {
	        particle->size = ofRandom(5.0f, 8.0f);
	        particle->color = ofColor(0, 0, 255);
	    }
	    // 🔵 NUEVO TIPO
	    else if (type == "nebula") {
	        particle->size = ofRandom(6.0f, 10.0f);
	        particle->color = ofColor(200, 0, 255);
	        particle->velocity *= 0.5f;
	    }
	    return particle;
	}
	
	ofApp::~ofApp() {
	    for (Particle * p : particles) { removeObserver(p); delete p; }
	    particles.clear();
	}
	
	void ofApp::setup() {
	    ofBackground(0);
	    particles.reserve(100 + 5 + 10);
	
	    for (int i = 0; i < 100; ++i) {
	        Particle * p = ParticleFactory::createParticle("star");
	        particles.push_back(p); addObserver(p);
	    }
	    for (int i = 0; i < 5; ++i) {
	        Particle * p = ParticleFactory::createParticle("shooting_star");
	        particles.push_back(p); addObserver(p);
	    }
	    for (int i = 0; i < 10; ++i) {
	        Particle * p = ParticleFactory::createParticle("planet");
	        particles.push_back(p); addObserver(p);
	    }
	
	    // 🔵 NUEVAS PARTÍCULAS
	    for (int i = 0; i < 8; ++i) {
	        Particle * p = ParticleFactory::createParticle("nebula");
	        particles.push_back(p);
	        addObserver(p);
	    }
	}
	
	void ofApp::update() {
	    for (Particle * p : particles) { p->update(); }
	}
	
	void ofApp::draw() {
	    for (Particle * p : particles) { p->draw(); }
	}
	
	void ofApp::keyPressed(int key) {
	    switch (key) {
	    case 's': notify("stop"); break;
	    case 'a': notify("attract"); break;
	    case 'r': notify("repel"); break;
	    case 'n': notify("normal"); break;
	
	    // 🔵 NUEVA TECLA
	    case 'w': notify("wave"); break;
	
	    default: break;
	    }
	}


EVIDENCIA 1:
<img width="1218" height="576" alt="image" src="https://github.com/user-attachments/assets/6ff51d96-6dc4-467e-9eae-681797689ee7" />
Coloqué un breakpoint en la función createParticle, específicamente en la rama correspondiente al tipo "nebula", ya que este es el punto donde se configura el nuevo tipo de partícula. Al avanzar en la ejecución, se observa que el objeto particle adquiere un tamaño dentro del rango definido (entre 6 y 10) y una velocidad reducida. Esto confirma que la factory está creando correctamente el nuevo tipo de partícula con sus propiedades diferenciadas.


EVIDENCIA 2:
<img width="1203" height="788" alt="image" src="https://github.com/user-attachments/assets/839e48f1-6dd9-45b8-9d7a-93d4da88cf93" />
Inspeccioné el puntero state en el depurador después de activar el nuevo estado WaveState. Al expandir el objeto, se observa que el _vfptr apunta a una dirección distinta en memoria y contiene funciones como WaveState::update y WaveState::onEnter. Al comparar con NormalState, se evidencia que las funciones virtuales cambian, lo que confirma que cada estado tiene su propia _vtable. Esto demuestra el uso correcto del polimorfismo, ya que el comportamiento de la partícula depende del tipo de estado activo.


EVIDENCIA 3:

<img width="1269" height="710" alt="image" src="https://github.com/user-attachments/assets/d02f4601-3f07-471a-837f-7a8789d0b417" />
Coloqué un breakpoint en el método keyPressed, específicamente en el caso de la tecla 'w', ya que este es el punto donde se genera el evento que activa el nuevo estado. Al ejecutar el programa y presionar la tecla correspondiente, se observa que se llama correctamente a notify("wave"), lo que confirma que el evento se origina desde la entrada del usuario.


<img width="1032" height="633" alt="image" src="https://github.com/user-attachments/assets/b95ee219-380a-49e1-b22f-23ac147d3c1d" />
Coloqué un breakpoint en el método onNotify, ya que este es el punto donde las partículas reciben el evento enviado por el sistema Observer. En el depurador se observa que el valor de event es "wave", lo que confirma que el evento generado en keyPressed se transmitió correctamente a través de notify y llegó a cada partícula.



<img width="1230" height="680" alt="image" src="https://github.com/user-attachments/assets/e00c9fa6-0b31-414c-b9c8-ee3f46c6ce8d" />
Finalmente, al ejecutar la instrucción setState(new WaveState()), se observa en el depurador que el puntero state cambia de NormalState a WaveState. Esto confirma que el evento "wave" no solo se transmite correctamente a través del patrón Observer, sino que también provoca un cambio real en el estado de la partícula, completando la cadena desde la entrada del usuario hasta la modificación del comportamiento.


EVIDENCIA 4:
<img width="1245" height="613" alt="image" src="https://github.com/user-attachments/assets/d078d111-1080-445d-956c-0f344d49a1f6" />
Coloqué un breakpoint en la sección donde se ejecuta el cambio al nuevo estado, ya que este es el punto donde se puede verificar si la partícula realmente adopta el comportamiento definido en WaveState. En el depurador se observa que el puntero state ahora apunta a WaveState, y al expandirlo se pueden ver sus funciones propias como update y onEnter, lo que demuestra que el estado tiene un comportamiento independiente.
Decidí que WaveState heredara directamente de la clase base State para poder definir un comportamiento completamente independiente y distinto a los otros estados. Esto permite mantener el código modular y fácil de extender, ya que se pueden agregar nuevos estados sin modificar los existentes. Además, al tener su propia _vtable, se garantiza que el comportamiento se resuelve dinámicamente en tiempo de ejecución, lo que es una ventaja clave del polimorfismo.


## Bitácora de aplicación 


## Bitácora de reflexión
