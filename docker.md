# **Docker en docker compose**

## **Docker en containers: basisconcepten**

### **Wat is Docker?**

Docker is een platform dat de ontwikkeling, implementatie en uitvoering van applicaties in zogenaamde "containers" vereenvoudigt. Containers zijn lichtgewicht, draagbare, zelfstandige omgevingen waarin software kan draaien. Zo hoef je niet eerst alles te downloaden en in te stellen, dit is van tevoren gedaan. https://www.docker.com/

### **Belangrijke Docker-concepten**

- **Image**: Een sjabloon dat wordt gebruikt om containers te maken. Docker images bevatten de code, bibliotheken, en configuratie voor een applicatie.
- **Container**: Een instantie van een image. Wanneer je èèn image maakt kan je bijvoorbeeld 10 verschillende geisoleerde containers hiervan naast elkaar draaien.
- **Docker Compose**: Een tool om applicaties die meerdere containers nodig hebben te beheren. Zo heb je maar 1 bestand nodig om alle benodigde containers te beheren en aan elkaar te kopellen.
- **Volume**: Een plek om data te bewaren van de containers, zelfs als je de container opnieuw opstart

**Waarom gebruiken we Docker voor onze LLM-omgeving?**

1. **Isolatie**: Ollama en Open WebUI draaien in geïsoleerde omgevingen zonder conflicten met andere software.
2. **Eenvoudige installatie**: Geen complexe configuratie.
3. **Consistentie**: De setup werkt hetzelfde op verschillende machines.
4. **Eenvoudige updates**: Updates kunnen worden toegepast door simpelweg nieuwe container-images te downloaden.

### **Docker installeren**

1. Installeer benodigde pakketten
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

2. Voeg Docker's officiële GPG-sleutel toe
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

3. Voeg Docker repository toe
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

4. Update pakketbronnen en installeer Docker
```bash 
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```
5. Voeg je gebruiker toe aan de docker-groep (geen sudo nodig voor docker-commando's)
```bash
sudo usermod -aG docker $USER
```

6. Start en enable Docker service
```
sudo systemctl start docker
sudo systemctl enable docker
```

Log uit en weer in (of herstart) om de groepswijzigingen toe te passen.

### **NVIDIA Container Toolkit configureren**

Om Docker-containers toegang te geven tot de GPU, moet de NVIDIA Container Toolkit worden geïnstalleerd:

1. Installeer de NVIDIA Container Toolkit
```bash
sudo apt-get install nvidia-container-toolkit -y
```

2. Configureer Docker voor gebruik met NVIDIA
```bash
sudo nvidia-ctk runtime configure --runtime=docker
```

3. Herstart Docker om de wijzigingen toe te passen
```bash
sudo systemctl restart docker
```

Test of de GPU beschikbaar is in Docker:

```bash
docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi
```

Als dit commando de GPU-informatie toont (vergelijkbaar met de eerdere nvidia-smi uitvoer), is de configuratie succesvol.

## **LLM-omgeving opzetten met Docker Compose**

### **Docker Compose configuratie**

1. Maak een nieuwe map voor je LLM-project:
```bash
mkdir ~/llm-setup
cd ~/llm-setup
```

Maak een docker-compose.yml bestand met [deze inhoud](docker-compose.yml)

**Toelichting bij deze configuratie:**

- Er worden twee containers opgezet:
  - **Ollama**: De backend die de LLM-modellen beheert en uitvoert
  - **Open WebUI**: De gebruiksvriendelijke webinterface voor interactie
- Volumes zorgen ervoor dat gegevens bewaard blijven, zelfs als de containers worden gestopt of verwijderd
- De GPU-toegang wordt geconfigureerd via het deploy gedeelte
- Open WebUI communiceert met Ollama via de interne Docker-netwerkverbinding

### **Opstarten van de omgeving**

Start de containers met het volgende commando:

```bash
docker-compose up -d
```

Dit commando start de containers in de achtergrond (`-d` voor "detached mode").

Na het opstarten is de webinterface beschikbaar op [http://localhost:3000](http://localhost:3000).

### **Containers beheren**

Nuttige commando's voor het beheren van je Docker-containers:

- Containers starten
```bash
docker-compose up -d
```

- Status van containers controleren
```bash
docker-compose ps
```

- Logs bekijken van de containers\
```bash
docker-compose logs -f ollama # Logs van Ollama
```
```bash
docker-compose logs -f ollama-webui # Logs van Open WebUI
```

- Containers stoppen
```bash
docker-compose stop
```

- Containers stoppen en verwijderen (data blijft behouden in volumes)
```bash
docker-compose down
```

- Containers stoppen en verwijderen inclusief volumes (WAARSCHUWING: alle data wordt verwijderd)
```bash
docker-compose down -v
```
