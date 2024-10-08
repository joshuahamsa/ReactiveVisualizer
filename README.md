# ReactiveVisualizer

![ReactiveVisualizer Logo](https://github.com/joshuahamsa/ReactiveVisualizer/blob/main/logo.png?raw=true)

**ReactiveVisualizer** is a comprehensive Python library designed to generate stunning reactive audio visualizer videos. Whether you're a musician wanting to create engaging visuals for your tracks or a developer looking to experiment with audio-visual synchronization, ReactiveVisualizer offers a versatile and modular framework to bring your creative visions to life.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Visualization Styles](#visualization-styles)
- [Audio Effects](#audio-effects)
- [Advanced Usage](#advanced-usage)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Features

- **Multiple Visualization Styles**: Choose from bar graphs, waveforms, circular plots, 3D visualizations, particle effects, generative art, and stereo visualizations.
- **Audio Effects**: Enhance your visuals with beat detection, real-time audio effects, metadata annotations, and live visualizations.
- **Customization**: Easily configure colors, number of bars, frames per second (FPS), resolution, and more via YAML configuration files or programmatically.
- **Integration with External Data**: Incorporate real-world data sources like Twitter trends or weather information to influence your visuals dynamically.
- **AI-Driven Enhancements**: Utilize machine learning models for advanced visual effects such as style transfer.
- **Support for Various Audio Formats**: Process multiple audio formats including MP3, WAV, FLAC, and M4A.
- **Export Options**: Generate videos in multiple formats like MP4 and GIF with customizable resolutions.
- **Modular Architecture**: Extend and customize the library by adding new visualizer modules or audio effects.

## Installation

### Prerequisites

- Python 3.7 or higher
- [FFmpeg](https://ffmpeg.org/download.html) installed and added to your system's PATH.

### Clone the Repository

```bash
git clone https://github.com/joshuahamsa/ReactiveVisualizer.git
cd ReactiveVisualizer
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

> **Note**: Installing `pyaudio` might require additional steps depending on your operating system. Refer to the [requirements.txt](#requirementstxt) section for detailed instructions.

### Install the Library

```bash
pip install -e .
```


## Quick Start

1. **Prepare Your Audio Files**

   Place all your album's audio files in a designated input directory, e.g., `./album_audio`.

2. **Configure Settings**

   Modify the `config/default_config.yaml` file to set your preferred input and output directories, visualization styles, effects, and other parameters.

   ```yaml
   input_dir: "path/to/your/album_audio"
   output_dir: "path/to/save/videos"
   fps: 30
   n_bars: 64
   color_scheme: "viridis"
   visualization_styles:
     - bar_graph
     - waveform
     - particle_effects
     - circular
     - three_d
     - generative_art
     - stereo_visualization
   enable_effects:
     - beat_detection
     - audio_effects
     - metadata_annotations
     - live_visualization
   export_formats:
     - mp4
     - gif
   resolution:
     width: 1920
     height: 1080
   ```

3. **Run the Example Script**

   Navigate to the `examples/` directory and execute the basic usage script.

   ```bash
   python examples/basic_usage.py
   ```

   This will process all audio files in the specified `input_dir` and generate corresponding video files in the `output_dir`.

## Configuration

ReactiveVisualizer uses YAML configuration files for easy customization. Here's an overview of the configurable parameters:

- **Directories**
  - `input_dir`: Path to the directory containing your audio files.
  - `output_dir`: Path where the generated videos will be saved.

- **Visualization Settings**
  - `fps`: Frames per second for the output video.
  - `n_bars`: Number of bars or elements in the visualizer.
  - `color_scheme`: Color scheme for visualizations (e.g., viridis, magenta, cyan).

- **Visualization Styles**
  - `visualization_styles`: List of visualization styles to include. Options:
    - `bar_graph`
    - `waveform`
    - `particle_effects`
    - `circular`
    - `three_d`
    - `generative_art`
    - `stereo_visualization`

- **Audio Effects**
  - `enable_effects`: List of audio effects to apply. Options:
    - `beat_detection`
    - `audio_effects`
    - `metadata_annotations`
    - `live_visualization`

- **Export Settings**
  - `export_formats`: Video formats to export (e.g., mp4, gif).
  - `resolution`: Video resolution settings (`width` and `height`).

- **Advanced Settings**
  - Additional parameters for specific visualizers or effects can be added as needed.

## Visualization Styles

### 1. Bar Graph

Displays a dynamic bar graph reacting to the audio spectrum.

### 2. Waveform

Visualizes the audio waveform with a moving cursor indicating the current playback position.

### 3. Particle Effects

Generates particle systems that respond to audio frequencies, creating flowing and dynamic visuals.

### 4. Circular

Creates radial bar graphs for an engaging circular representation of the audio data.

### 5. 3D Visualization

Implements 3D bar graphs that rotate and provide an immersive visual experience.

### 6. Generative Art

Produces procedurally generated fractal patterns that evolve over time based on the audio spectrum.

### 7. Stereo Visualization

Separates and visualizes left and right audio channels, offering a stereo-specific display.

## Audio Effects

### Beat Detection

Synchronizes visual effects precisely with the music's beats, enhancing impactful moments.

### Audio Effects

Applies real-time audio processing effects like reverb or echo to influence the visualization dynamically.

### Metadata Annotations

Overlays track information such as track name and artist onto the video.

### Live Visualization

Supports real-time audio input, enabling live performances or streaming visualizations.

## Advanced Usage

### Customizing via API

Instead of using configuration files, you can customize ReactiveVisualizer programmatically.

```python
from reactive_visualizer import ReactiveVisualizer

def main():
visualizer = ReactiveVisualizer()
visualizer.config['input_dir'] = "path/to/your/album_audio"
visualizer.config['output_dir'] = "path/to/save/videos"
visualizer.config['visualization_styles'] = ['bar_graph', 'waveform']
visualizer.process_album()
if __name__ == "__main__":
    main()
```


### Extending with New Visualizers or Effects

ReactiveVisualizer is built with a modular architecture. To add a new visualizer:

1. **Create a New Module**

   Add a new Python file in the `visualizers/` directory, e.g., `new_visualizer.py`.

2. **Implement the Visualizer Class**

   ```python
   # ReactiveVisualizer/visualizers/new_visualizer.py
   import matplotlib.pyplot as plt

   class NewVisualizer:
       def __init__(self, config):
           # Initialize with config
           pass

       def generate_frame(self, spectrum, current_time):
           # Implement visualization logic
           frame_filename = f"frames/new_visualizer_frame_{int(current_time * 1000)}.png"
           plt.savefig(frame_filename)
           plt.close()
           return frame_filename
   ```

3. **Register the Visualizer**

   Update `visualizers/__init__.py` to include the new visualizer.

   ```python
   from .new_visualizer import NewVisualizer

   __all__ = [
       # ... other visualizers
       'NewVisualizer'
   ]
   ```

4. **Configure Usage**

   Add the new visualizer to the `visualization_styles` list in your YAML configuration or set it programmatically.

## Contributing

Contributions are welcome! Whether it's bug fixes, new features, or enhancements to the documentation, your support helps make ReactiveVisualizer better for everyone.

### Steps to Contribute

1. **Fork the Repository**

2. **Create a New Branch**

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**

4. **Commit Your Changes**

   ```bash
   git commit -m "Add feature: your feature description"
   ```

5. **Push to the Branch**

   ```bash
   git push origin feature/your-feature-name
   ```

6. **Open a Pull Request**

   Provide a clear description of your changes and any relevant details.

### Code of Conduct

Please adhere to the [Code of Conduct](https://github.com/joshuahamsa/ReactiveVisualizer/blob/main/CODE_OF_CONDUCT.md) in all interactions.

## License

This project is licensed under the [MIT License](https://github.com/joshuahamsa/ReactiveVisualizer/blob/main/LICENSE).

## Acknowledgements

- [Librosa](https://librosa.org/) for audio analysis.
- [Matplotlib](https://matplotlib.org/) for visualization.
- [MoviePy](https://zulko.github.io/moviepy/) for video processing.
- [Pyaudio](https://people.csail.mit.edu/hubert/pyaudio/) for audio streaming.
- [TensorFlow](https://www.tensorflow.org/) for AI-driven enhancements.
- Open-source contributors who have made this project possible.

---
