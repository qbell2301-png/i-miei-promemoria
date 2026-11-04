# I miei promemoria — web app personale

## Cosa contiene
- PWA responsive in tema scuro, installabile su Android.
- Promemoria, scadenze, ricorrenze, avvisi anticipati, lista attività e note.
- Dati salvati nel browser del dispositivo.
- Service worker predisposto per ricevere notifiche push.

## Avvio rapido (solo anteprima locale)
Dalla cartella del progetto avvia un server statico HTTPS (o localhost). Per esempio:
`npx serve .`
Apri l'indirizzo dal telefono. Per installarla: menu del browser → Aggiungi a schermata Home.

## Importante: notifiche ad app chiusa
La PWA include il service worker e un server push Node nella cartella `server/`, ma le notifiche push reali non si attivano semplicemente aprendo il file HTML. Servono:
1. Pubblicare la parte web su un dominio HTTPS.
2. Avviare il server `server/` su un hosting Node sempre attivo.
3. Generare le chiavi VAPID con `npm run vapid` dentro `server/`.
4. Impostare `VAPID_PUBLIC_KEY`, `VAPID_PRIVATE_KEY`, `VAPID_SUBJECT` e un `ADMIN_TOKEN` segreto nell'hosting.
5. Collegare il pulsante di attivazione alla registrazione push e all'endpoint `/api/subscribe`, quindi inviare gli impegni pianificati a `/api/schedule` con l'autorizzazione Bearer.

Il server è una base tecnica per la consegna push; questa prima versione non è ancora collegata automaticamente al server. Le notifiche locali in pagina aperta sono best-effort e non sono affidabili quando il browser viene chiuso. Le notifiche push su Android richiedono HTTPS, consenso esplicito e configurazione server.

## Privacy e dati
Attività e note sono salvate in `localStorage` sul browser del dispositivo. Non sincronizzano automaticamente tra dispositivi. Non inserire informazioni particolarmente sensibili.
