# Eduna
C'est un projet de mise en place d'un chatbot basé adapté à la réalité africaine dans le cadre de la bibliotheque numérique EduNiger permettant de faciliter encore plus l'apprentissage.

# 1 Installation de Ubuntu sur Termux
## Étape 1 : Installer Termux et ses dépendances
pkg update && pkg upgrade -y
pkg install proot-distro -y
## Installer Ubuntu via Proot
proot-distro install ubuntu
## Étape 3 : Lancer Ubuntu
proot-distro login ubuntu
# 2 Installation des dépendances
## Étape 4 : Mettre à jour Ubuntu
apt update && apt upgrade -y
## Étape 5 : Installer Python et pip
apt install python3 python3-pip -y
## Étape 6 : Installer venv sans ensureepip
apt install python3.10-venv -y
python3 -m venv --without-pip myenv
source myenv/bin/activate
curl https://bootstrap.pypa.io/get-pip.py | python
## Étape 7 : Installer openai et requests
pip install requests requests
# Installation du chatbot(Eduna)
## Étape 8 : Cloner le projet ou créer main.py
import requests
import json

# Remplace par ta clé OpenRouter
API_KEY = "TON_CLE_API"

API_URL = "https://openrouter.ai/api/v1/chat/completions"
HEADERS = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json",
}

def chat_with_gpt(messages):
    payload = {"model": "openai/gpt-3.5-turbo", "messages": messages}
    try:
        response = requests.post(API_URL, headers=HEADERS, json=payload)
        response.raise_for_status()
        return response.json()"choices"][0]["message"]["content"]
    except requests.exceptions.RequestException as e:
        return f"Erreur lors de la requête : {e}"

if __name__ == "__main__":
    print("Bienvenue sur le chatbot Eduna ! (Tape 'exit' pour quitter)\n")
    chat_history = [{"role": "system", "content": "Tu es un assistant intelligent."}]

    while True:
        user_input = input("Toi: ")
        if user_input.lower() == "exit":
            print("Fin de la session.")[
            break

        chat_history.append({"role": "user", "content": user_input})
        response = chat_with_gpt(chat_history)
        chat_history.append({"role": "assistant", "content": response})

        print(f"Eduna: {response}\n")
  ## Exécuter le chatbot
  python main.py
