# React-Router-Dom: Visão Geral
A primeira coisa a fazer é criar um `Browser Router` e configurar nossa primeira rota.

```js
  import React from "react";
  import ReactDOM from "react-dom/client";
  import {
    createBrowserRouter,
    RouterProvider,
  } from "react-router-dom";
  import "./index.css";

  const router = createBrowserRouter([
    {
      path: "/",
      element: <div>Hello world!</div>,
    },
  ]);

  ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
    <React.StrictMode>
      <RouterProvider router={router} />
    </React.StrictMode>
  );
```