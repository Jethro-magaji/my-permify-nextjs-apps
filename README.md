## A Fullstack Next.js Application with [Permify](https://docs.permify.co/setting-up/installation/intro)

This repository showcases a basic implementation of Role-Based Access Control (RBAC) using [Permify](https://docs.permify.co/setting-up/installation/intro) in a Next.js application with an Express.js backend. It demonstrates how to define roles, permissions, and user relationships in Permify and use them to control access to different parts of the application.

### Project Structure

```
my-permify-nextjs-app/
├── public/
|   ├── next.svg
│   └── vercel.svg
├── app/
│   ├── api
│   │   └── permission.js
|   ├── page.js
│   ├── admin.js
│   ├── error.js
│   ├── index.js
|   ├── member.js
│   ├── manager.js
|   ├── layout.js
│   └── global.css
├── app.js
├── app-relationship.js
├── app-tenant.js
├── app-schema.js
├── package.json
├── tailwind.config.js
├── jsconfig.json
├── package-lock.json
├── postcss.config.mjs
└── next.config.mjs  
```

**File Descriptions:**

* **`app/`:** Contains all Next.js pages:
    * **`app/api/`:** Next.js API routes:
        * **`app/api/permission.js`:** Handles authorization checks using Permify and sends responses to the frontend.
    * **`app/admin.js`:** Component for the dashboard page, accessible only to admins.
    * **`app/error.js`:** Component for the error page, shown when unauthorized.
    * **`app/page.js`:**  This is the landing page with login buttons for different roles.
    * **`app/manager.js`:** Component for the manager page, accessible to managers and admins.
    * **`app/member.js`:** Component for the member page, accessible to members, managers, and admins.
* **`next.config.mjs`:**  Next.js configuration file.
* **`package.json`:**  Project dependencies.
* **`app-tenant.js`:** Configuration for Permify tenant.
* **`app-schema.js`:**  Defines the Permify schema with entities, roles, and permissions.
* **`app.js`:**  Express.js backend server file handling API routes and authorization logic.

### Getting Started

1.  **Install Dependencies:**

    ```bash
    npm install
    ```

2.  **Start the Permify Server (Docker):**
    You can run Permify Service with [various options](https://docs.permify.co/setting-up/installation/intro#deployment-guides) but in that tutorial we run it via docker container. 

    Production usage of Permify needs some configurations such as defining running options, selecting datastore to store authorization data and more. 

    However, for the sake of this tutorial we'll not do any configurations and quickly start Permify on your local with running the docker command below:

    ```shell
    docker run -p 3476:3476 -p 3478:3478  ghcr.io/permify/permify serve
    ```

    This will start Permify with the default configuration options: 
    * Port 3476 is used to serve the REST API.
    * Port 3478 is used to serve the GRPC Service.
    * Authorization data stored in memory.

    #### Test your connection

    You can test your connection with creating an HTTP GET request,

    ```shell
    localhost:3476/healthz
    ```

3.  **Configure Permify:**
    *   Replace `"your-tenant-id"` with your actual tenant ID.
    *   Run `node app-schema.js` to write the schema to Permify.
    *   Run `node app-permission.js` to grant the `admin` role access to the `organization` entity.

4.  **Start the Backend Server:**

    ```bash
    node app.js
    ```

5.  **Start the Next.js Development Server:**

    ```bash
    npm run dev
    ```

6.  **Access the Application:** Navigate to `http://localhost:3000/` in your browser.

### Usage

*   Enter a User ID in the input field on the `index.js` page.
*   Click the "Login" button for your desired role (Admin, Member, or Manager).
*   The application will send a request to the `permission` API route for authorization.
*   If authorized, you'll be redirected to the corresponding page.
*   If unauthorized, you'll be redirected to the `error` page.

### Key Features

*   **Role-Based Access Control:** Users are assigned roles (admin, manager, member) with different permissions.
*   **Permify Integration:**  Uses the `@permify/permify-node` and `@permify/react-role` libraries to implement authorization checks.
*   **Next.js Routing:**  Handles client-side routing using `next/navigation`.
*   **Express.js Backend:** Provides API routes for authorization checks.
*   **Tailwind CSS:**  Uses Tailwind CSS for styling the frontend app.

### Notes

*   **Authentication:**  This example uses simulated user data and authentication for demonstration purposes.  Replace it with your actual authentication system.
*   **API Routes:** You will likely need to implement more robust API routes to handle user data, authorization, and other application logic.

### Contributing

Contributions are welcome!  Feel free to submit pull requests for bug fixes, feature enhancements, or documentation improvements.

### License

This project is licensed under the MIT License.