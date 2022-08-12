## Config Inertia:

composer require inertiajs/inertia-laravel

php artisan inertia:middleware

Thêm vào trong file App\Http\Kernel

```php
'web' => [
    // ...
    \App\Http\Middleware\HandleInertiaRequests::class,
],
```

Chạy command

composer require tightenco/ziggy
npm install
npm install @inertiajs/inertia @inertiajs/inertia-vue3
npm install @inertiajs/progress

thêm vào trong file vite.config.js phía sau Laravel()

```js
import vue from '@vitejs/plugin-vue';

vue({
    template: {
        transformAssetUrls: {
            base: null,
            includeAbsolute: false,
        },
    },
})
```

Thêm vào trong resources/js/app.js

```js
import './bootstrap';
import '../css/app.css';

import { createApp, h } from 'vue';
import { createInertiaApp } from '@inertiajs/inertia-vue3';
import { InertiaProgress } from '@inertiajs/progress';
import { resolvePageComponent } from 'laravel-vite-plugin/inertia-helpers';
import { ZiggyVue } from '../../vendor/tightenco/ziggy/dist/vue.m';

const appName = window.document.getElementsByTagName('title')[0]?.innerText || 'Laravel';

createInertiaApp({
    title: (title) => `${title} - ${appName}`,
    resolve: (name) => resolvePageComponent(`./Pages/${name}.vue`, import.meta.glob('./Pages/**/*.vue')),
    setup({ el, app, props, plugin }) {
        return createApp({ render: () => h(app, props) })
            .use(plugin)
            .use(ZiggyVue, Ziggy)
            .mount(el);
    },
});

InertiaProgress.init({ color: '#4B5563' });
```

Tạo view ở trong resource/Pages và render với Inertia::render ở controller