# Bintana

**Desktop applications with visual forms and plain JavaScript, on GTK4.**

Bintana is a RAD environment in the spirit of Visual Basic and Gambas: you draw
a form, double-click a button, and write what it does. Forms are laid out by
coordinates, there is one class per form, and handlers wire themselves up by
name. The engine is [QuickJS](https://github.com/getbintana/quickjs) embedded
in a GTK4 runtime written in C.

```js
class Form1 extends Form {
    Button1_Click() {
        Message.Info("Hello, {0}!", this.TextBox1.Text);
    }
}
```

No imports, no bundler, no build step for the code: a project is a folder with
a `project.json`, its `.form` files and their `.js`, and `bintana <folder>`
runs it.

**The IDE is written in Bintana and runs on the same runtime**, with no
privileges and no private API. When it needs something the runtime lacks, what
gets added is a feature every application then has.

## Repositories

### The runtime

| | |
|---|---|
| [**bintana**](https://github.com/getbintana/bintana) | The runtime, the IDE, the shipped libraries and the examples. Start here. |
| [**quickjs**](https://github.com/getbintana/quickjs) | Our fork of [QuickJS-ng](https://github.com/quickjs-ng/quickjs), vendored by the runtime as a submodule. |

### Writing an application

| | |
|---|---|
| [**bintana-docs**](https://github.com/getbintana/bintana-docs) | The reference: one page per control, per global and per library component, the `.form` format and the designer. The IDE's F1 help comes from here. |
| [**bintana-llm**](https://github.com/getbintana/bintana-llm) | Everything needed to write a complete application **without the IDE**: `llm.txt`, a step-by-step guide and examples that run. Made for language models, and just as useful to people. |
| [**bintana-taglib**](https://github.com/getbintana/bintana-taglib) | A native plugin wrapping TagLib, and the reference for writing a plugin of your own in C. |

### Applications

| | |
|---|---|
| [**bintana-project**](https://github.com/getbintana/bintana-project) | **Bintana Project**: opens, edits and writes back MS Project (MSPDI XML) files, with a task tree beside an interactive Gantt chart, calendars, resources, costs and the critical path. |

### Packaging

| | |
|---|---|
| [**flatpak**](https://github.com/getbintana/flatpak) | Builds the Bintana BaseApp and every registered application, and publishes them as a Flatpak repository. |
| [**windows**](https://github.com/getbintana/windows) | Builds a Windows installer for every registered application, tests it and attaches it to a release. |

Both read the same registry: adding an application to them is adding one
`app.json`.

## Install

**Linux, as a Flatpak:**

```sh
flatpak remote-add --if-not-exists --no-gpg-verify bintana \
    https://getbintana.github.io/flatpak/
flatpak install bintana io.github.getbintana.Ide        # the IDE
flatpak install bintana io.github.getbintana.Project    # Bintana Project
```

**Windows:** the IDE's installer and a portable zip are in the
[runtime's releases](https://github.com/getbintana/bintana/releases); the
applications' installers are in the
[windows releases](https://github.com/getbintana/windows/releases).

**From source:**

```sh
git clone --recurse-submodules https://github.com/getbintana/bintana.git
cd bintana
cmake -S . -B build && cmake --build build -j
./build/bintana ide examples/hello
```

It needs GTK 4.10 or newer, GtkSourceView 5, a C compiler, CMake and
pkg-config; [installing.md](https://github.com/getbintana/bintana/blob/main/docs/installing.md)
has the package names per distribution.

## License

The runtime, the IDE and Bintana Project are MIT, as is the vendored
QuickJS-ng.
