# limpiar-browser-navegador
Script que limpia el navegador para probar mejor.


    (async function limpiarNavegadorL10() {
        console.clear();
        console.log('%c /* 🐹 */ INICIANDO LIMPIEZA PROFUNDA LIDERTECH...', 'background: #222; color: #bada55; font-size: 14px;');
    
        // 1. Limpiar almacenamiento de texto
        localStorage.clear();
        sessionStorage.clear();
        console.log('✅ LocalStorage y SessionStorage: ¡LIMPIOS!');
    
        // 2. Limpiar IndexedDB (por si Firebase o Angular guardaron algo ahí)
        const dbs = await window.indexedDB.databases();
        dbs.forEach(db => window.indexedDB.deleteDatabase(db.name));
        console.log('✅ Bases de datos IndexedDB: ELIMINADAS');
    
        // 3. Limpiar Cache Storage (Imágenes y assets cacheados por el navegador)
        if ('caches' in window) {
            const cacheNames = await caches.keys();
            await Promise.all(cacheNames.map(name => caches.delete(name)));
            console.log('✅ Cache de Imágenes/Assets: BORRADO');
        }
    
        // 4. Forzar recarga completa desde el servidor (Hard Reload)
        console.log('%c 🚀 Reiniciando aplicación en 1 segundo...', 'color: #00ff00');
        setTimeout(() => {
            window.location.reload(true);
        }, 1000);
    })();
