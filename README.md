# flac2m4a

Script to convert FLAC albums to gapless M4A AAC on macOS via the built-in `afconvert` utility.

## Dependencies

| Dependency | Purpose | Installation |
| ---------- | ------- | ------------ |
| `afconvert`| M4A AAC conversion | comes with macOS |
| `ffmpeg` | for exporting tags from FLAC files | `brew install ffmpeg` |
| `AtomicParsley` | for writing tags to M4A files | `brew install AtomicParsley` |

## Usage

```
flac2m4a -o output_dir -- input_dir1 input_dir2 ...
```

- Input folder structure is preserved
- jpg/gif/png files are copied to the output tree as is
- FLAC files are converted to M4A and copied to the output tree
- FLAC files in the same input folder are converted gaplessly
- Parallelized up to the number of CPU cores via `sysctl -n hw.ncpu`

## Example

Given this folder structure:

```
├── "Chimp Orchestra - Zoo Symphony No. 1"
│   ├── "CD1"
│   │   ├── "1 - Chimp Orchestra - Movement 1.flac"
│   │   └── "2 - Chimp Orchestra - Movement 2.flac"
│   ├── "CD2"
│   │   ├── "1 - Chimp Orchestra - Movement 3.flac"
│   │   ├── "2 - Chimp Orchestra - Movement 4.flac"
│   │   └── "3 - Chimp Orchestra - Movement 5.flac"
│   └── "folder.jpg"
└── "Chimp Orchestra - Zoo Symphony No. 2"
    ├── "1 - Chimp Orchestra - Movement 1.flac"
    ├── "2 - Chimp Orchestra - Interlude.flac"
    ├── "3 - Chimp Orchestra - Movement 2.flac"
    └── "folder.jpg"
```

If we run `flac2m4a -o m4a -- *`, we get the following structure:

```
├── "Chimp Orchestra - Zoo Symphony No. 1"
│   ├── "CD1"
│   │   ├── "1 - Chimp Orchestra - Movement 1.flac"
│   │   └── "2 - Chimp Orchestra - Movement 2.flac"
│   ├── "CD2"
│   │   ├── "1 - Chimp Orchestra - Movement 3.flac"
│   │   ├── "2 - Chimp Orchestra - Movement 4.flac"
│   │   └── "3 - Chimp Orchestra - Movement 5.flac"
│   └── "folder.jpg"
├── "Chimp Orchestra - Zoo Symphony No. 2"
│   ├── "1 - Chimp Orchestra - Movement 1.flac"
│   ├── "2 - Chimp Orchestra - Interlude.flac"
│   ├── "3 - Chimp Orchestra - Movement 2.flac"
│   └── "folder.jpg"
└── "m4a"
    ├── "Chimp Orchestra - Zoo Symphony No. 1"
    │   ├── "CD1"
    │   │   ├── "1 - Chimp Orchestra - Movement 1.m4a"
    │   │   └── "2 - Chimp Orchestra - Movement 2.m4a"
    │   ├── "CD2"
    │   │   ├── "1 - Chimp Orchestra - Movement 3.m4a"
    │   │   ├── "2 - Chimp Orchestra - Movement 4.m4a"
    │   │   └── "3 - Chimp Orchestra - Movement 5.m4a"
    │   └── "folder.jpg"
    └── "Chimp Orchestra - Zoo Symphony No. 2"
        ├── "1 - Chimp Orchestra - Movement 1.m4a"
        ├── "2 - Chimp Orchestra - Interlude.m4a"
        ├── "3 - Chimp Orchestra - Movement 2.m4a"
        └── "folder.jpg"
```
