self.addEventListener('install',e=>self.skipWaiting());
self.addEventListener('activate',e=>e.waitUntil(self.clients.claim()));
self.addEventListener('push',e=>{let data={title:'I miei promemoria',body:'Hai un nuovo avviso.'};try{data={...data,...e.data.json()}}catch{}e.waitUntil(self.registration.showNotification(data.title,{body:data.body,icon:'/icon.svg',badge:'/icon.svg',data:{url:'/'}}))});
self.addEventListener('notificationclick',e=>{e.notification.close();e.waitUntil(clients.matchAll({type:'window',includeUncontrolled:true}).then(list=>{for(const c of list)if('focus'in c)return c.focus();return clients.openWindow('/')}))});
