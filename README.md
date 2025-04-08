# fkie_measurement_sensor_simulator

## Description

This package allows to simulate environmental sources such us hot-spots or radioactive elements. It assumes the measurements are continuously distributed across the space using a (configurable) propagation function.

## Demo:

Launch a basic simulation setup with three hot-spots and an static sensor:

```
ros2 launch fkie_measurement_sensor_simulator sensor_simulator.launch.xml
```

## Usage

- Sensor simulator node:

``` xml
  <arg name="global_frame" default="world"/>
  <arg name="sensor_frame" default="sensor_frame"/>

  <node name="sensor_simulator" pkg="fkie_measurement_sensor_simulator" exec="sensor-simulator">
    <param from="$(find-pkg-share fkie_measurement_sensor_simulator)/config/sensor_simulator_config.yaml" />
    <param name="global_frame" value="$(var global_frame)"/>
    <param name="sensor_frame" value="$(var sensor_frame)"/>
    <param name="rate" value="2.0"/>
    <param name="marker_size" value="0.4"/>
    <param name="topic_measurement" value="measurement"/>

    <param name="unique_serial_id" value="ASD-123"/>
    <param name="manufacturer_device_name" value="Dummy Thermometer Device"/>
    <param name="device_classification" value="M"/>

    <param name="sensor_name" value="sensor_1"/>
    <param name="sensor_source_type" value="temperature"/>
    <param name="sensor_unit" value="C"/>

    <param name="utm_zone_number" value="32"/>
    <param name="utm_zone_letter" value="U"/>
    <param name="random_pos_factor" value="2.5"/>
  </node>

  <node name="tf_world_sensor_frame" pkg="tf2_ros" exec="static_transform_publisher" args="367260.37 5609547.24 255 0 0 0 $(var global_frame) $(var sensor_frame)">
  </node>
```

- Example Config file ```sensor_simulator_config.yaml```:

``` yaml
/**:
  ros__parameters:
    sources/source_0/name: "hot-spot 1"
    sources/source_0/intensity: 10.0
    sources/source_0/x: 367258.37
    sources/source_0/y: 5609545.24
    sources/source_0/z: 255.
    sources/source_0/function: "linear"
    sources/source_0/linear_alpha: 5.0
    sources/source_0/color_rgba: [0.0, 0.7, 0.0, 0.8] 
    sources/source_0/text_color_rgba: [0.8, 0.8, 0.8, 0.8]

    sources/source_1/name: "hot-spot 2"
    sources/source_1/intensity: 10.0
    sources/source_1/x: 1.0
    sources/source_1/y: 3.0
    sources/source_1/z: 1.0
    sources/source_1/function: "inverse_squared"
    sources/source_1/linear_alpha: 5.0
    sources/source_1/color_rgba: [0.0, 0.0, 0.7, 0.8]
    sources/source_1/text_color_rgba: [0.8, 0.8, 0.8, 0.8]

    sources/source_2/name: "hot-spot 3"
    sources/source_2/intensity: 10.0
    sources/source_2/x: 2.0
    sources/source_2/y: 2.0
    sources/source_2/z: 1.0
    sources/source_2/function: "exponential"
    sources/source_2/exponential_decay_rate: 3.0
    sources/source_2/color_rgba: [0.7, 0.0, 0.0, 0.8]
    sources/source_2/text_color_rgba: [0.8, 0.8, 0.8, 0.8]
```

## Contributors

```
Alexander Tiderko
alexander.tiderko@fkie.fraunhofer.de
Francisco J. Garcia R.
```