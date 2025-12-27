# HISE Stereo Panner

A stereo panner effect built with HISE ScriptNode, demonstrating channel splitting and crossfade control techniques.

## Overview

This project implements a stereo panner that splits the input signal into left and right channels and controls their gain in opposite directions. When the left channel gain increases, the right channel gain decreases, and vice versa.

## Features

- **Stereo Channel Splitting**: Separates input into independent L/R channels
- **Crossfade Control**: Smooth panning using RMS curves for proper decibel handling
- **Intuitive Range**: Pan parameter ranges from -1 (full left) to +1 (full right)

## ScriptNode Architecture

### Nodes Used

- **1x `container.multi`**: Handles the channel splitting (renamed to "ChannelSplit")
- **1x `control.xfader`**: Controls the crossfade between left and right channels
- **2x `core.gain`**: Individual gain controls for each channel

### Signal Flow

```
Input → control.xfader → container.multi (ChannelSplit)
                              ├─ core.gain (Left)
                              └─ core.gain (Right)
```

The `control.xfader` generates two modulation sources that inversely control the gain of each channel. The crossfade curves are set to RMS mode for proper decibel-based panning.

## Parameters

| Parameter | Range | Description |
|-----------|-------|-------------|
| Pan | -1 to +1 | Controls stereo position (-1 = full left, 0 = center, +1 = full right) |

## Getting Started

### Prerequisites

- HISE audio framework
- Basic understanding of ScriptNode

### Installation

1. Clone this repository
2. Open the project in HISE
3. Load the ScriptNode network
4. Connect the Pan parameter to your GUI

### Usage

1. Add the network to your HISE project
2. Create a Pan knob in your interface
3. Set the knob's range to -1...+1
4. Connect it to the Pan parameter in the network

## Configuration

The crossfade curves are set to **RMS mode** to ensure proper gain scaling in decibels. To verify or change this:

1. Right-click on the `control.xfader` node
2. Select the curve type from the menu
3. Choose "RMS" for decibel-based crossfading

## Technical Notes

- The signal flow visualization shows stereo cables connecting each node
- Modulation targets are labeled "1" and "2" and controlled by the xfader
- The container.multi node enables parallel processing of L/R channels

## HISE Snippet

Import this snippet directly into HISE:

```
HiseSnippet 1321.3oc6X0rbaaCDFTRPwxIoMYZe.zQmYRzPJqDaO8Pc7OJUSic3X55o2x.SBYgQj.bHghsZmduuUsOR8MncW9iHnirislIoWhNYr6hc+v9yG.sahxmmlpRHVcNcdLmX8Hp2bodx9SXBIYzADquk5o4IbUWWlTxSH6MOlklxCHVVMeCZjUmVjre+yOtGKjI84UhHjyTBe9aEQBckT2c+YQX3PV.+TQjg0C1cjuRtuJTMC.TSpMIl4OkcA+XFZVCJwp8gABsJwSyz7ThUq8VAy8lntTla+YhTw4gbbgCwCbTt3gpv.DwnTx9SDgAtkG7TB3E2pzPy7zv2SORDHVHuJc7jLEcq1gY9vpQc30rF7bLgmsA7VBjrLfTqbH8TpmehHVWoAwyCoijP8YLCR6lPI2Vh0eS2WAFH08hXS4CSfEK1vF86a+7tN8se1OLdlzWKTxtJ4wJM+cxMd15+95cV+OVu60UMd7R0ggIQEFxSVpZrRmbaabC4rny4IOu6GXgy3KCDN90yozaNmZVx8yO0FFpjijB86h4xapQfTjpv7eAp.S0YY+uoH66EJBfo.Ajj6PmJUmCiEjLHa10S9kQGvzrRGA9DhSLOQKvif0A7O.SE4k0NzC3oS0p3LaihURDAVctCg8ppPNZ24UKNXWM+JvGqQKlYipMl9WQhffPtqJUfk.SbGWlMFAAZ8hsO7JXNLAFAg1FTNEkCSweTGJLanBlExz0GXPVhBEX3L6RwVQI.i4lrHWeJp0caJ51Gxuqv8oTWg1exxwaikfWnF+4FuEbROld33wbecEXaQG9q2JAz8FJ2Uxn0K5Kg3i.wnUYYjP+IsZfONgCcS7SUtgr4ajxhhC4m.n84cOOT4O0S7a7OlknnubOzhM7mfwJLcUHSZemInctUBZxIpYZg7hiX5DALGROdVjGbskOe+BzAxrZfbJ4qsw0X2hGWFjs3egeEJcv0VEJcJUVQGQNlquTkLMqXT72PoHm++77KcGeE40ggpKQNDQQqKTBxj4pBmGOQIE9nnbKJA5qiTyPBmbzBtWE.m+1CY9PdZtKSOAGJP5TnqimzyeQ22RK5YMVPB0sjwHMOYhts7l87DA.inLpN7d8lnd730HO9TL.qQuZLCo8pAlmjAFnH2qPa8f+IBTKChXPRwJXdtQ9icf5nAzOKmXuIse1.ooosQ1CdoET5IG4A0uKQxiSYIWv0Y92TPwsARdVyZZ8kfCQji7qsou8vgmRbM4bamwhRNRHKB3ZzW3Xa2ylbD6pEX.WCuVKFGhv2vX2CrI6myfcrcbdEzTOkeYd5jX8czW1aP+982xdqsFr8.mMs2o9Q3th3GPOYza9o+2frQACIqJWAE6pfmGIyH6.qwB4Cn4hd8LsJBnEJojqtBXQ8jXzb9XJN.wC8hCg21diiKQyB0h6WK5RmEJZJpEmGBwIg26BLMeuhPiZYrlFYr1e9KW4mlrdiqmxWNPtdoaMJFy6GPPC1z1wdSvfc1Y6A6rksSw6m8hTJ8DfKubVtMsO5cxW9zxinmvS45b2Wy4DSZKy1vxQuu1X70Fi5Lg2rl5bjn+yeRe0YoMbVVBc4hqCsu8KFZUdwvhavqcyPIi6mhct1IH6UnlW.+H5nzyPs9rvRjAugYU9xquHulKh4mndewaWvCzZYRfzoL6euQG5Q35tNkeNYdRA9XMw588wG6+BXRX46o+JrmMWg8LXE1yKWg87pUXOasB6Y6acO3+omClHrsFD3dXVykk0gRF7cBYejC4+.r0rCQC
```

## Resources

- [HISE Documentation](https://docs.hise.dev/)
- [ScriptNode Tutorial Series](https://docs.hise.dev/scriptnode/101/)
- [Original Tutorial](https://docs.hise.dev/scriptnode/101/panner.html)

## Author

Tutorial by Matt_SF (21.11.2021)

## License

Please refer to the HISE framework license for usage terms.