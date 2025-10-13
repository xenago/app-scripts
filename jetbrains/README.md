# jetbrains

JetBrains/IntelliJ/RustRover IDEs.

## Switching Rust versions in RustRover

RustRover still can't properly deal with `rustup` on its own to manage versions, it requires manual pain.

To change the Rust verison used by a project:

1. List available toolchains

       rustup toolchain list

2. Install desired toolchain, if not available

       rustup toolchain install 1.89.0

3. Switch to the desired toolchain

       rustup default 1.89.0

4. Install the sources component

       rustup component add rust-src

5. Open the RustRover Settings, under `Rust > Standard library` set to `/home/<user>/.rustup/toolchains/<toolchain>/lib/rustlib/src/rust`
