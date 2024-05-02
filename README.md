<p align="center">
  <a href="https://www.clerk.dev/?utm_source=github&utm_medium=starter_repos&utm_campaign=remix_auth_starter" target="_blank" align="center">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="./docs/clerk-logo-dark.png">
      <img src="./docs/clerk-logo-light.png" height="64">
    </picture>
  </a>
  <br />
</p>

# GetAuth Error reproduction

The issue we are facing is that `getAuth` doesn't seem to return the user if invoked right after signin in. In our repository, we use a sign in custom flow so this reproduction is not 100% accurate - that said, the specific issue seems to affect sign-in via `<SignIn />` as well.

The issue happens if we navigate to a route with a loader calling `getAuth` right after we log in. To do this, I set `forceRedirectUrl='/ssr-demo'` on the `SignIn` component inside `sign-in.$.tsx`.

To reproduce it yourself:

- download the repo & install deps
- login via password
- verify that after login, the user is redirected to `/ssr-demo` and immediately redirected back to the login page - this happens because `getAuth` doesn't detect the authenticated user and therefore redirects back to the login page

![Shot Arc -2024-05-02 at 12 56 57](https://github.com/elledienne/clerk-getauth-repro/assets/3903093/39b60533-776c-47fc-b945-f94140fd0c6b)
