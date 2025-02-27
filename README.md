# DM13A breakout board

Breakout board for the DM13A LED driver, for use with MobiFlight. This is completely untested and not intended for real-world use. The goal of this repo was to explore using KiCad 9 command line tools to automate releases of the design, including schematics, board images, and JLCPCB fabrication files.

## Highlights

Highlights

- A VSCode devcontainer is included that includes the `kicad-cli` command for local development.
- A `tasks.json` file is included to enable quick local testing of the jobset generation.
- Outputs are defined using KiCad [jobsets](https://docs.kicad.org/9.0/en/kicad/kicad.html#jobsets).
- Variables are used to specify a version and date stamp. These are used in the sheet data blocks as well as the silkscreen on the board.
- A GitHub [workflow](https://github.com/neilenns/dm13a-breakout-board/blob/main/.github/workflows/release.yaml) runs when a GitHub release is created, or when triggered manually, to produce all the output files. The version variable is set to the GitHub release version and the date stamp is set to the year, month, and day of the GitHub release.
- Output files are modified by the workflow to match the JLCPCB upload requirements.
- The completed outputs are uploaded to the [release](https://github.com/neilenns/dm13a-breakout-board/releases) for easy access.
- Board images are automatically checked in to the docs directory via an auto-merged pull request, for use in this readme.

## Generated outputs

- [Schematic](https://github.com/neilenns/dm13a-breakout-board/releases/latest/download/dm13a-breakout-board-schematic.pdf)
- [Documentation zip](https://github.com/neilenns/dm13a-breakout-board/releases/latest/download/dm13a-breakout-board-documentation.zip), including schematic and PCB images
- [JLCPCB submission zip](https://github.com/neilenns/dm13a-breakout-board/releases/latest/download/dm13a-breakout-board-JLCPCB.zip), including gerbers, drill position, BOM, and CPL files

![Front of board](docs/dm13a-breakout-board-top.png)

## Using this in your own project

For everything to work correctly the GitHub repository name must exactly match the KiCad project name. For example, this repo is named `dm13a-breakout-board` and the project is `dm13a-breakout-board.kicad_pro`.

> [!IMPORTANT]
> The workflow and jobset depend on the GitHub repository and KiCad project name being exactly the same. If they don't match,
> none of this will work.

Copy the following two files into the same location in your repository:

- `.github/workflows/release.yaml`: The GitHub workflow for releases.
- `jobs.kicad_jobset`: The jobset that defines the outputs required for the release.

In your project, use the `VERSION` variable wherever the version number should get placed, and the `DATE` variable wherever the date should be placed.

To make a new release simply use the GitHub release feature. The resulting files will get attached to the release, and the updated board images will be merged into the `docs/` folder of the repo.

Don't forget that KiCad has [integrated git commands](https://docs.kicad.org/9.0/en/kicad/kicad.html#git_integration) for committing and pushing changes!
