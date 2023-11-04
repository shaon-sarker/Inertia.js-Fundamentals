
# Introduction to Inertia.js
# Principles
#### Pages that are served by the server
#### Interaction between the client and the server
#### The API does not have any endpoints
#### Data sharing

# Use Cases
#### Applications based on monoliths:
#### Applications built with Laravel and Rails:
#### Validating forms and forms
#### Optimizing SEO

# Comparison of SSR and CSR
Rendering web content on the server (SSR) and on the client (CSR) are two fundamental approaches. Unlike CSR, which relies on client-side JavaScript to generate content dynamically, SSR processes content on the server and sends a fully rendered page to the client.

SSR delivers pre-rendered content, enhancing initial page load performance and improving SEO. It ensures that search engines can crawl and index content accurately, benefiting discoverability. However, SSR can be computationally intensive on the server, potentially leading to slower response times for complex applications.

CSR, on the other hand, delivers a lightweight initial page and uses JavaScript to fetch and render data dynamically. This results in a faster initial load time for simpler applications. Yet, CSR may lead to SEO challenges, as search engines might not interpret JavaScript-heavy content optimally. Additionally, CSR may not be suitable for content-rich or highly interactive sites, as they can suffer from slower load times and less efficient SEO.

#  Inertia.js Features:
**Server-Driven Pages:**

**Explanation:** Inertia.js follows a server-driven approach, where most rendering logic resides on the server. This means that each request to the server returns a full HTML response, including layout and content.
Example: When a user navigates to a different page, the server sends a complete HTML response, reducing the need for client-side routing.

**Client-Side Interactivity:**

**Explanation:** Despite the server-driven approach, Inertia.js enables client-side interactivity using JavaScript. This is achieved by sending XHR (XMLHttpRequest) requests to the server for data or actions without full page reloads.
Example: When a user clicks a button to update their profile picture, Inertia.js sends an XHR request to the server to update the image without refreshing the entire page.

**No API Endpoints:**

**Explanation:** Inertia.js eliminates the need to create separate API endpoints for client-server communication. It uses existing server-side routes and controllers.
Example: Instead of setting up dedicated API routes, Inertia.js utilizes the existing server routes for handling actions like form submissions.

# Integration with Laravel
**Step 01: Install Laravel**

If you haven't already, install Laravel using Composer:
```bash
composer create-project --prefer-dist laravel/laravel inertia-example
```

**Step 02: Install the Inertia.js Adapter**

Install the Inertia.js adapter for Laravel:
```bash
 composer require inertiajs/inertia-laravel
```

**Step 03: Set Up Routes and Controllers**

Create a controller and set up a route to handle your page:
```bash
 php artisan make:controller PageController
```
In **PageController.php** create a method to handle your page:
```bash
 public function index()
{
    return Inertia::render('Welcome', [
        'name' => 'John Doe',
    ]);
}
```

**Step 04: Create a Blade Template**

Create a **Blade template (resources/views/welcome.blade.php)** to render your Inertia.js page::
```bash
<!DOCTYPE html>
<html>
<head>
    <title>Welcome</title>
    <meta name="csrf-token" content="{{ csrf_token() }}">
    <link href="{{ mix('/css/app.css') }}" rel="stylesheet">
    <script src="{{ mix('/js/app.js') }}" defer></script>
</head>
<body>
    @inertia
</body>
</html>

```
**Step 05: Create a Vue Component**

Create a **Vue component (resources/js/Pages/Welcome.vue)** for your page::
```bash
<template>
  <div>
    <h1>Hello, {{ name }}!</h1>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
  },
};
</script>

```

**Step 06: Set Up Client-Side Routes**

Edit **resources/js/app.js** to set up client-side routes:
```bash
import { createApp, h } from 'vue';
import { createInertiaApp } from '@inertiajs/inertia-vue3';

createInertiaApp({
  resolve: name => require(`./Pages/${name}.vue`),
  setup({ el, App, props }) {
    createApp({ render: () => h(App, props) }).use(store).use(router).mount(el);
  },
});

```
**Step 07: Run Your Application**

IStart your Laravel development server:
```bash
 php artisan serve
```

# Client-Side Components

Using Vue.js with Inertia.js: A Seamless Integration

Vue.js and Inertia.js complement each other, offering a powerful blend of server-driven rendering and client-side interactivity. Here's how they work together:

**Inertia.js for Server-Driven Pages:**
Inertia.js primarily handles server-driven rendering. When a user navigates to a page, the server sends a full HTML response, including layout and content. This ensures fast initial page loads and improves SEO.
#### Vue.js for Client-Side Interactivity:
While Inertia.js handles the initial page load, Vue.js takes over for client-side interactivity. It's responsible for dynamic updates without requiring full page reloads. Vue components enhance the user experience by providing interactive elements.
#### Data Exchange:
Inertia.js facilitates data exchange between the server and client. When the server renders a page, it can pass data to the client. This shared data can be used to dynamically update the page without requiring additional requests to the server.
### Client-Side Components:
Vue.js components are utilized for client-side interactivity. These components can include forms, buttons, modals, and other interactive elements. They're designed to enhance the user experience by providing dynamic and responsive features.
#### Example: Editing a User Profile:
Let's consider an example where a user wants to edit their profile information:

**Server-Side Rendering (Inertia.js):**

The server renders the initial profile page using Inertia.js. It includes the user's name, email, and other details.

**Client-Side Interactivity (Vue.js):**

When the user clicks the "Edit" button, a Vue.js component is activated. This component allows the user to make changes to their profile.

**Data Exchange:**

Vue.js components can send XHR (XMLHttpRequest) requests to the server to update the user's information. The server processes this request and returns a response with the updated data.

**Dynamic Updates:**

The Vue.js component dynamically updates the page to reflect the changes made by the user. This is done without requiring a full page refresh.
By combining Vue.js and Inertia.js, developers can create web applications that offer a seamless user experience. The server-driven approach ensures fast initial page loads and optimal SEO, while Vue.js components provide interactivity and dynamic updates, resulting in a modern and responsive application.
