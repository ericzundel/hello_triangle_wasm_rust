# Hello Triangle with WebGL and Rust

This is a minimal example that demonstrates how to render a triangle with WebAssembly, WebGL, Rust, and zero dependencies.  There's a tutorial that goes along with this example at [rust-tutorials.github.io](https://rust-tutorials.github.io/triangle-from-scratch/web_stuff/web_gl_with_bare_wasm.html)

To build the project perform the following steps:

1. Install Rust.
2. Install the `wasm32-unknown-unknown` target: `rustup target add wasm32-unknown-unknown`
3. Build the directory: `cargo build --target wasm32-unknown-unknown`
4. Run a local server to host the project directory.  If you are running VSCode, you can just launch `index.html` in the preview pane.

## Installing a local web server

If you aren't using VSCode you will need some other web server installed to view the example.

### Using Python as a web server

If you have python installed, you can use this one-liner from the root of your local copy of this repo:

`python3 -m http.server 8080`

or

`python -m SimpleHTTPServer 8080`

Navigate to `localhost:8080` in your web browser and view the triangle!

### Using devserver

You can try using a minimal webserver for development `devserver`:

* First run `cargo install devserver`
* Then simply run `devserver`.
* Navigate to `localhost:8080` in your web browser and view the triangle!

Note that if your system uses opensslv3, you may encounter errors from the SSL library about unspported RC2-40-CBC algorithm due to the self-signed certificate used by this binary.

## How to create a smaller .wasm file

The `.wasm` file produced under `target/wasm32-unknown-unknown/debug` is around 1.4mb. Which is kinda big!

Now you can run a build a *release* build with most of the compiler information stripped out:

`cargo build --target wasm32-unknown-unknown --release`

You must change this line in `index.html` to `fetch('target/wasm32-unknown-unknown/release/hello_triangle_wasm_rust.wasm')` to make sure it points to the release folder.

This new stripped .wasm file is 22kb instead of 1.4mb. Less than 2% the original size!
