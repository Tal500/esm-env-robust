# esm-env-robust

Like [esm-env](https://github.com/benmccann/esm-env), uses export conditions to return environment information in a way that works with major bundlers and runtimes,
 but this project is also 'robust' in the sense it have also a fallback bahaviour for older environments that doesn't support
 the `exports` fields in `package.json`.

This project was motivated to solve issue [esm-env#1](https://github.com/benmccann/esm-env/issues/1), but works for wider audience.

Demo of fallback in old environment: https://svelte.dev/repl/6ae4871d6a48460fb8be28afaf9a6e1d?version=3.54.0

## Usage

1. Install with `npm install esm-env-robust`.
2. Import according to the desired behaviour:
    * If you want to detect only whether the environment is the browser or not, use:
    ```js
        import { BROWSER } from 'esm-env-robust';
    ```
    * If you (also) need to check whether the environment is production or development, you need to specify what is the fallback
     behaviour for older environment by the import path:
        * If the desired fallback is that `DEV` will be `false`, use:
        ```js
        import { DEV, BROWSER } from 'esm-env-robust/dev-fallback-false';
        ```
        * If the desired fallback is that `DEV` will be `true`, use:
        ```js
        import { DEV, BROWSER } from 'esm-env-robust/dev-fallback-true';
        ```

If you don't care about fallback behaviour for older environments at all, consider using the basic [esm-env](https://github.com/benmccann/esm-env) package instead.

## Fallback value of `BROWSER`

The fallback value of `BROWSER` is set up **on runtime** by checking the value of `typeof window`.
Currently, code minification tools, as far as we know, don't optimize this value to compile time.
That means you enjoy the most of both worlds by using this package - on updated environments you'll get the correct value on compile time, and on older environments you'll get the correct value on runtime (better than nothing).

## License

[MIT](LICENSE)
