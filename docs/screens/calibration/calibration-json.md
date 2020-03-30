---
tags: [Survey]
---

# Calibration JSON file example

В данном JSON из необходимых полей это:
"commands", "mode", "screen_size", "window_rect"

- commands - описывает данные по каждой точке(координаты и время в какое она показана на экране относительно времени старта калибровки)

## [Sync doc](../../../docs/screens/sync.md)

```json
{
  "commands": [
    {
      "type": "set_calibration_data",  - static value
      "value": [ - tracking point position data
        [
          [180, 326.3333435058594],
          38
        ]
      ]
    }
  ],
  "mode": "calibration",
  "screen_size": [
    360, - width
    720 - height
  ],
  "window_rect": {
    "window_x": 0, - static value
    "window_y": 24, - status bar height
    "window_width": 360, - (Math.ceil(window.width / 2) * 2)
    "window_height": 654 -(Math.ceil(window.height / 2) * 2) - bar_height
  },
  "sensors": {
    "rotations": [
      {
        "o": 0, - degree
        "t": 0 -timestamp
      }
    ],
    "gyroscope": [ - gyroscope data
      {
        "x": "-0.001",
        "y": "0.000",
        "z": "0.000",
        "t": 4868
      }
    ],
    "accelerometer": [
      {
        "x": "0.779",
        "y": "0.129",
        "z": "10.061",
        "t": 4736
      }
    ]
  }
}
```