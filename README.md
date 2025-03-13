# Reverb-Real-Time-Notifications
 I will show you how to send real-time notifications with Reverb in the laravel 11 application.

### Project run process
```bash
git clone https://github.com/ruhulamin63/Reverb-Real-Time-Notifications.git
```

```bash
composer install
or
composer update
```

```bash
cp .env.example .env
```

```bash
php artisan migrate
```

```bash
npm run dev
or
npm run build
```

```bash
php artisan serve
```

### Using public ip
```bash
http://localhost:8000/login //post route for admin access

http://localhost:8000/login // post route for user access
```

 ### Setup Reverb & Echo Server
Now, we need to configure laravel broadcast and Reverb as driver.

So, first by default laravel has not enabled broadcasting, so you need to run the following command to enable it.
```bash
php artisan install:broadcasting
```

laravel will ask to install Reverb and you need to select "Yes". then it will automatically installed it.

You need to run the following commands to install Reverb. it's option if you already selected yes then.
```bash
composer require laravel/reverb
```

```bash
php artisan reverb:install
```

Now, we will install laravel echo server, so, let's run the below commands:
```bash
npm install --save-dev laravel-echo
```

now, you will see some code on the echo.js file, where you can made a changes:

- resources/js/echo.js
```bash
import Echo from 'laravel-echo';

import Pusher from 'pusher-js';
window.Pusher = Pusher;

window.Echo = new Echo({
    broadcaster: 'reverb',
    key: import.meta.env.VITE_REVERB_APP_KEY,
    wsHost: import.meta.env.VITE_REVERB_HOST,
    wsPort: import.meta.env.VITE_REVERB_PORT ?? 80,
    wssPort: import.meta.env.VITE_REVERB_PORT ?? 443,
    forceTLS: (import.meta.env.VITE_REVERB_SCHEME ?? 'https') === 'https',
    enabledTransports: ['ws', 'wss'],
});
```

Then, set the BROADCAST_CONNECTION environment variable to Reverb in your application's .env file, also we will add Reverb env variables:

```bash
BROADCAST_CONNECTION=reverb

REVERB_APP_ID=256980
REVERB_APP_KEY=f4l2tmwqf6eg0f6jz0mw
REVERB_APP_SECRET=zioqeto9xrytlnlg7sj6
REVERB_HOST="localhost"
REVERB_PORT=8080
REVERB_SCHEME=http

VITE_REVERB_APP_KEY="${REVERB_APP_KEY}"
VITE_REVERB_HOST="${REVERB_HOST}"
VITE_REVERB_PORT="${REVERB_PORT}"
VITE_REVERB_SCHEME="${REVERB_SCHEME}"
```
