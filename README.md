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

o `router` define um Elemento que vai ser renderizado como a "rota padrão" da sua aplicação.

# React-Router-Dom: ErrorElement
o `errorElement` é o elemento padrão renderizado quando uma rota não existente é chamada na aplicação. ele é definido no `router`.

```js
const router = createBrowserRouter([
  {
    path: "/",
    element: <Root />,
    errorElement: <ErrorPage />,
  },
]);
```

enquanto o elemento que vai ser renderizado pode ter contido o elemento `useRouteError` que dá detalhes do erro que foi lançado. 

```js
  import { useRouteError } from "react-router-dom";

  export default function ErrorPage() {
    const error: any = useRouteError();
    console.error(error);

    return (
      <div id="error-page">
        <h1>Oops!</h1>
        <p>Sorry, an unexpected error has occurred.</p>
        <p>
          <i>{error.statusText || error.message}</i>
        </p>
      </div>
    );
  }
```
# React-Router-Dom: Criando novas rotas
A criação de uma nova rota é como a adição de um novo objeto no array `router`. Esse array leva o `path: string` e o `element: <div />`. 

```js
  /* existing imports */
  import Contact from "./routes/contact";

  const router = createBrowserRouter([
    {
      path: "/",
      element: <Root />,
      errorElement: <ErrorPage />,
    },
    {
      path: "contacts/:contactId",
      element: <Contact />,
    },
  ]);
```

# React-Router-Dom: Criando uma rota filha
A criação de uma rota filha extende os componentes de sua rota pai, ela traz consigo tudo que o pai possue e adiciona tudo que a rota filha possue.

```js
  const router = createBrowserRouter([
    {
      path: "/",
      element: <Root />,
      errorElement: <ErrorPage />,
      children: [
        {
          path: "contacts/:contactId",
          element: <Contact />,
        },
      ],
    },
  ]);
```
Para renderizar uma rota filha, é necessário definir "aonde" essa rota deve ser renderizada. Definimos isso com `<Outlet>` 

```js
import { Outlet } from "react-router-dom";

export default function Root() {
  return (
    <>
      {/* all the other elements */}
      <div id="detail">
        <Outlet />
      </div>
    </>
  );
}
```
# React-Router-Dom: Usando o Elemento <Link />
Quando usamos um link carregado pelo elemento `<a/>`, podemos notar que oque acontece é uma re-renderização completa da página, o navegador está solicitando um documento completo para a próxima URL em vez de usar o React Router.
o Elemento `<Link />` serve para evitar que esse recarregamento desnecessário, substituindo o `<a />`. Impede tambem que o link acabe gerando URLs como `contacts/contacts/1`.

```js
  <Link to={`contacts/1`}>Your Name</Link>
```
