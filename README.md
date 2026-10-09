# Study Buddy — Frontend

Interface React/Vite pour le chatbot Study Buddy : streaming des réponses, sélecteur de modèle, notes personnelles, Stop / retry, affichage des tokens.

**Backend :** https://github.com/princesse-aku/bootcamp-chatbot-backend

**En ligne :** https://bootcamp-chatbot-frontend-delta.vercel.app  
(API : https://api-production-a6ef8.up.railway.app)

## Lancer en local

1. Démarrer le backend sur `http://localhost:8000`.
2. Puis :

```bash
npm install
npm run dev
```

Ouvrir `http://localhost:5173`. Le proxy Vite renvoie `/api/*` vers le backend (pas de CORS en local).

### Production / front déployé

Créer un `.env` (non commité) :

```
VITE_API_URL=https://votre-backend.example
```

## Fonctionnalités UI

- **Streaming** : `fetch` + `ReadableStream` (`getReader`), pas `EventSource` (POST).
- **Modèle** : liste via `GET /models`, envoyé à chaque `POST /chat`.
- **Notes** : case « Mode note » → `POST /conversations/{id}/notes` (jamais au LLM).
- **Stop** : `AbortController` — le tour n'est pas sauvegardé.
- **Réessayer** : après une erreur LLM, bouton pour renvoyer le même message.
- **Tokens** : champ `usage` relayé dans l'événement SSE `meta`.
