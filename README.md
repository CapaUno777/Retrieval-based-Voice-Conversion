<div align="center">

<h1>Retrieval-based-Voice-Conversion</h1>
An easy-to-use Voice Conversion framework based on VITS.<br><br>

[![madewithlove](https://img.shields.io/badge/made_with-%E2%9D%A4-red?style=for-the-badge&labelColor=orange
)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion)

<img src="https://counter.seku.su/cmoe?name=rvc&theme=r34" /><br>

[![Licence](https://img.shields.io/github/license/RVC-Project/Retrieval-based-Voice-Conversion?style=for-the-badge)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion/blob/develop/LICENSE)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

</div>

------


> [!NOTE]
> Currently under development... Provided as a library and API in rvc

## Installation and usage

### CLI Usage

#### Inference Audio

```sh
rvc infer -m {model.pth} -i {input.wav} -o {output.wav}
```

| option        | type         | default value | description                                                                                                                                                                                                                                    | require |
|---------------|--------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| modelPath     | Path         |               | Model path or filename (reads in the directory set in env)                                                                                                                                                                                     | *       |
| inputPath     | Path         |               | Input audio path or folder                                                                                                                                                                                                                     | *       |
| outputPath    | Path         |               | Output audio path or folder                                                                                                                                                                                                                    | *       |
| sid           | int          | 0             | Speaker/Singer ID                                                                                                                                                                                                                              |         |
| f0_up_key     | int          | 0             | Transpose (integer, number of semitones, raise by an octave: 12, lower by an octave: -12)                                                                                                                                                      |         |
| f0_method     | str          | rmvpe         | pitch extraction algorithm (pm, harvest, crepe, rmvpe                                                                                                                                                                                          |         |
| f0_file       | Path \| None | None          | F0 curve file (optional). One pitch per line. Replaces the default F0 and pitch modulation                                                                                                                                                     |         |
| index_file    | Path \| None | None          | Path to the feature index file                                                                                                                                                                                                                 |         |
| index_rate    | float        | 0.75          | Search feature ratio (controls accent strength, too high has artifacting)                                                                                                                                                                      |         |
| filter_radius | int          | 3             | If >=3: apply median filtering to the harvested pitch results. The value represents the filter radius and can reduce breathiness                                                                                                               |         |
| resample_sr   | int          | 0             | Resample the output audio in post-processing to the final sample rate. Set to 0 for no resampling                                                                                                                                              |         |
| rms_mix_rate  | float        | 0.25          | Adjust the volume envelope scaling. Closer to 0, the more it mimicks the volume of the original vocals. Can help mask noise and make volume sound more natural when set relatively low. Closer to 1 will be more of a consistently loud volume |         |
| protect       | float        | 0.33          | Protect voiceless consonants and breath sounds to prevent artifacts such as tearing in electronic music. Set to 0.5 to disable. Decrease the value to increase protection, but it may reduce indexing accuracy                                 |         |