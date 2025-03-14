# **Hardware**

Voor een functionele LLM-omgeving is de grafische kaart (GPU) het belangrijkste onderdeel. Hoe meer videogeheugen beschikbaar is, hoe grotere modellen kunnen worden ingeladen, grotere modellen presteren beter dan kleinere.

### **Onze configuratie**

Wij hebben voor deze configuratie gekozen aangezien op moment van bestelling (December 2024), dit een goede prijs-kwaliteit verhouding was. Uiteraard kan je afwijken van deze specificaties.

Tip: Kijk op tweakers voor de meest actuele prijzen van computer hardware. https://tweakers.net/pricewatch/

- **GPU**: [INNO3D GeForce RTX 4070 SUPER TWIN X2](https://www.inno3d.com/products_detail.php?refid=909) (12GB VRAM)
  - Afhankelijk van prijsontwikkelingen kan een andere GPU voordeliger zijn
  - Voor zwaardere toepassingen kun je een GPU met meer geheugen overwegen
- **CPU**: Intel Core i5-12600K of vergelijkbaar
- **Moederbord**: ASUS PRIME B760-PLUS D4
- **RAM**: 64 GB DDR4 (bijv. Corsair Vengeance LPX CMK64GX4M2E3200C16)
- **Opslag**: 2TB NVMe SSD (bijv. WD Black SN770)
- **Voeding**: 750W of hoger (80+ Gold certificering aanbevolen)
- **Koeling**: CPU-koeler zoals Noctua NH-L12S
- **Behuizing**: Kies een mid-tower of full-tower met goede ventilatie

**Opmerking**: De modellen zelf zijn erg groot meerdere GBs. Zo kan een kleinere opslag snel vol raken. Ook wanneer je bestanden upload die de LLM moet gebruiken, worden die ook lokaal opgeslagen.

### **Hardware-keuzegids: welke GPU voor welke modellen?**

| GPU Model | VRAM | Max. Model Grootte | Aanbevolen Modellen | Geschatte Kosten |
|---|---|---|---|---|
| RTX 4060 | 8GB Tot 7B parameters | Gemma-7b, Phi-2, Qwen-7b | €300-€350 | 
| RTX 4070 Super | 12GB Tot 14B parameters | DeepSeek-R1-14b, Phi-3-mini, Qwen-14b | €550-€650 | 
| RTX 4080 | 16GB | Tot 20B parameters | Mistral-Large, Llama3-8x2 | €800-€1000 |
| RTX 4090 | 24GB | Tot 30-40B parameters | Llama-3-70b (quantized), Mixtral-8x7b | €1400-€1800 | 
| 2x RTX 4090 | 48GB | 70B+ parameters | DeepSeek-V2, Llama-3-70b | €2800-€3600 |

**Toelichting**: Kleinere modellen (7B) werken prima binnen een experimenteer omgeving.

### **Aandachtspunten bij hardware-selectie**

- **GPU-geheugen**: Dit bepaalt welke modellen je kunt draaien en hoeveel tegelijk.
- **Behuizing**: Kies een ruime behuizing met goede airflow voor adequate koeling.
- **Internetverbinding**: Een stabiele internetverbinding is noodzakelijk voor het downloaden van modellen en mogelijk om toegang te bieden aan gebruikers.
- **Stroomverbruik**: Krachtigere GPU's verbruiken meer stroom.

De totale kosten voor de aanbevolen configuratie liggen rond de €1.100, wat een eenmalige investering is in tegenstelling tot doorlopende abonnementskosten voor commerciële AI-diensten.