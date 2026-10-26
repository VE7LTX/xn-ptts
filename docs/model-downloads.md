# Model weights and voices

This fork stores the runtime source and this download guide, **not model binaries**. Use Gradium's official downloads below. Verified against upstream documentation and Hugging Face metadata on 2026-10-26; links are pinned where practical for reproducibility.

## Recommended starting point: English 31M

[Model card](https://huggingface.co/gradium/phonon-31m-en) · [All files](https://huggingface.co/gradium/phonon-31m-en/tree/main)

The public English model is Apache-2.0 licensed. The q8 weight file is 64,512,352 bytes (about 64.5 MB); supporting files and runtime storage are additional. Keep these files together in a local folder such as `phonon-31m-en/`:

| File | Official pinned download | Purpose |
| --- | --- | --- |
| `model.q8.gguf` | [Download](https://huggingface.co/gradium/phonon-31m-en/resolve/92741c5b07d085ff840e26fea8ce43110b87852f/model.q8.gguf) | q8 model weights |
| `config.json` | [Download](https://huggingface.co/gradium/phonon-31m-en/resolve/92741c5b07d085ff840e26fea8ce43110b87852f/config.json) | Model configuration |
| `tokenizer.json` | [Download](https://huggingface.co/gradium/phonon-31m-en/resolve/92741c5b07d085ff840e26fea8ce43110b87852f/tokenizer.json) | Runtime tokenizer |
| `tokenizer.model` | [Download](https://huggingface.co/gradium/phonon-31m-en/resolve/92741c5b07d085ff840e26fea8ce43110b87852f/tokenizer.model) | Tokenizer asset referenced in model configuration |
| `default-voice.safetensors` | [Download](https://huggingface.co/gradium/phonon-31m-en/resolve/92741c5b07d085ff840e26fea8ce43110b87852f/default-voice.safetensors) | Bundled default voice |

Model revision: `92741c5b07d085ff840e26fea8ce43110b87852f`.

Hugging Face's published LFS SHA-256 for `model.q8.gguf`:
`a7d9aad2cd6dc66473f24a08bc6d2939030ef4d751ef82349361fbef3272dbae`.
This is source metadata, not a locally recomputed checksum. Compare it with the downloaded file before use.

## Runtime options

Get the standalone executable from [official Gradium releases](https://github.com/gradium-ai/xn-ptts/releases), following the [CLI guide](cli.md), including its platform prerequisites and release checksums. The Windows/Linux desktop archives are CPU builds; GPU backends require a suitable source build. This guide does not claim benchmark results on any particular computer.

Once the standalone `ptts` executable is installed, this command fetches the pinned English checkpoint and caches it:

```sh
ptts --model hf://gradium/phonon-31m-en@92741c5b07d085ff840e26fea8ce43110b87852f --lang en --quant q8 "Hello from Phonon." -o speech.wav
```

Or use the manually downloaded folder:

```sh
ptts --model ./phonon-31m-en --lang en --quant q8 "Hello from Phonon." -o speech.wav
```

In PowerShell, use `.\ptts.exe` instead of `ptts` if the executable is in the current directory rather than on PATH. Local model folders require no Hub download. These commands are documented instructions, not tests executed for this fork.

## Optional additional voices

The default voice above is sufficient to start. [Gradium's voice catalog](https://huggingface.co/gradium/phonon-voices) provides names, IDs and playable samples; its metadata declares Apache-2.0. An extra catalog voice does not add a new spoken language to an English-only model.

Pinned catalog revision: `0ee17205f254b5abc43b266c8a0f215565c352f7`.

- [Catalog index: voices.jsonl](https://huggingface.co/gradium/phonon-voices/resolve/0ee17205f254b5abc43b266c8a0f215565c352f7/voices.jsonl)
- [Zoey, English US: NbpkqMVS3CJeq2j8.safetensors](https://huggingface.co/gradium/phonon-voices/resolve/0ee17205f254b5abc43b266c8a0f215565c352f7/voices/NbpkqMVS3CJeq2j8.safetensors)
- [Easton, English US: LMDIYE0Oa377Qh6Z.safetensors](https://huggingface.co/gradium/phonon-voices/resolve/0ee17205f254b5abc43b266c8a0f215565c352f7/voices/LMDIYE0Oa377Qh6Z.safetensors)

The standalone CLI accepts `--voice ./path/to/voice.safetensors`. With network access, `--voice Zoey` instead retrieves the named catalog voice when needed; `ptts --list-voices` lists available names. For a fully offline setup, download the selected voice first and use its local path. See [upstream voice instructions](../README.md#voices). Custom cloning is separate and requires the speaker's consent.

## Other models and licence boundaries

The [upstream model table](../README.md#model-setup) links the 40M English, French, German, Spanish, Portuguese and multilingual models. **All those 40M variants are CC BY-NC 4.0, including English**, unlike the Apache-2.0 31M English model. Their Hugging Face repositories are gated; access requires accepting their terms. This guide does not accept terms or configure credentials.

[40M multilingual model card](https://huggingface.co/gradium/phonon-40m-multilingual) · [CC BY-NC 4.0 licence](https://creativecommons.org/licenses/by-nc/4.0/) · [Apache-2.0 licence](https://www.apache.org/licenses/LICENSE-2.0)

Runtime code is separately MIT OR Apache-2.0. Review the model and voice terms before redistribution or commercial deployment. Do not commit access tokens or personal voice recordings to this public fork.

## Verification scope

Official model and voice repository revisions, filenames, sizes and licence metadata were checked. Direct download links were checked without fetching large model binaries. No model was installed, executed or benchmarked; weights remain hosted by Gradium on Hugging Face, so this is a reproducible reference rather than an independent binary backup.
