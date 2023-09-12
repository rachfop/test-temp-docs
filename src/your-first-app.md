# Your first app

# How to download the Temporal CLI

The Temporal CLI is available on the MacOs, Windows, and Linux.

Choose one of the following install methods to install the Temporal CLI.

<Tabs>

<TabItem value="macOS" label="macOS">

- Install the Temporal CLI with Homebrew.

```bash

brew install temporal

```

- Install the Temporal CLI with cURL.

```bash

curl -sSf https://temporal.download/cli.sh | sh

```

- Install the Temporal CLI from CDN.

1. Select the platform and architecture needed.

- <a href="https://temporal.download/cli/archive/latest?platform=darwin&arch=amd64">Download for Darwin amd64</a>

- <a href="https://temporal.download/cli/archive/latest?platform=darwin&arch=arm64">Download for Darwin arm64</a>

2. Extract the downloaded archive.

3. Add the `temporal` binary to your PATH.

</TabItem>

<TabItem value="Linux" label="Linux">

- Install the Temporal CLI with cURL.

```bash

curl -sSf https://temporal.download/cli.sh | sh

```

- Install the Temporal CLI from CDN.

1. Select the platform and architecture needed.

- <a href="https://temporal.download/cli/archive/latest?platform=linux&arch=amd64">Download for Linux amd64</a>

- <a href="https://temporal.download/cli/archive/latest?platform=linux&arch=arm64">Download for Linux arm64</a>

2. Extract the downloaded archive.

3. Add the `temporal` binary to your PATH.

</TabItem>

<TabItem value="Windows" label="Windows">

- Install the Temporal CLI from CDN.

1. Select the platform and architecture needed and download the binary.

- <a href="https://temporal.download/cli/archive/latest?platform=windows&arch=amd64">Download for Windows amd64</a>

- <a href="https://temporal.download/cli/archive/latest?platform=windows&arch=arm64">Download for Windows arm64</a>

2. Extract the downloaded archive.

3. Add the `temporal.exe` binary to your PATH.

</TabItem>

</Tabs>

- *Start the Temporal Development Server**

Start the Temporal Development Server by using the `server start-dev` command.

```bash

temporal server start-dev

```

This command automatically starts the Web UI, creates the default [Namespace](/namespaces), and uses an in-memory database.

The Temporal Server should be available on `localhost:7233` and the Temporal Web UI should be accessible at [`http://localhost:8233`](http://localhost:8233/).

The server's startup configuration can be customized using command line options.

For a full list of options, run:

```bash

temporal server start-dev --help

```