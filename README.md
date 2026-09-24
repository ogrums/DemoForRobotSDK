# DemoForRobotSDK

One screen of buttons that call `RobotSdk`. Compile it and run it on the robot. The screenshot is `docs/20240820-121954.jpeg`.

Power the servos first. Later moves do nothing until that has been done. The Chinese README line is "需要先上电启动舵机之后，后面的行动才可用".

## Entry

`com.geeui.demoforrobotsdk.MainActivity`

- `onCreate` calls `RobotService.getInstance(this)`
- `onDestroy` calls `unbindService()`
- The SDK is `app/libs/RobotSdk-release.aar`

There is no AIDL of its own, no serial port, and no cloud client. The SDK talks to the system services.

## Buttons

| Button | Label | Call |
|---|---|---|
| `fab` | 启动舵机 / start servos | `robotOpenMotor()` |
| `fab1` | 关闭舵机 / stop servos | `robotCloseMotor()` |
| `fab2` | 向前走 / walk forward | `ActionMessage` slot `[63, 2] = 3`, then `robotActionCommand` |
| `fab3` | 耳朵转动 / rotate ears | `AntennaMessage` `[3, 2, 300] = 60`, then `robotAntennaMotion` |
| `fab4` | 耳朵亮灯 / light the ears | `AntennaLightMessage.set(Light.RED)`, then `robotAntennaLight` |
| `fab5` | 监听传感器 / listen to sensors | `robotRegisterSensorCallback` |
| `fab6` | 解除监听 / stop listening | `robotUnregisterSensor()` |
| `fab7` | 测试tts / test TTS | `robotPlayTTs("你好你好")` |
| `fab8` | 打开sensor | `robotOpenSensor()` |
| `fab9` | 关闭sensor | `robotCloseSensor()` |
| `fab10` | 跳舞 / dance | `sendLongCommand("speechDance", "from_third")` |
| `fab11` | 显示充电图标 | `robotControlStatusBar(StatusBarCmd.COMMAND_SHOW_CHARGING)` |
| `fab12` | 隐藏充电图标 | `robotControlStatusBar(StatusBarCmd.COMMAND_HIDE_CHARGING)` |

`SensorCallback` only logs tap, double-tap, long-press, fall back, fall forward, fall right, fall left, and time-of-flight.

Calls present in the file but not wired to a button: `robotControlCommand`, `robotCloseAntennaLight`, `robotControlSound`, `robotStartExpression("h0280")`.

## Comment glossary

| Where | Chinese | English |
|---|---|---|
| README | 将程序编译运行到机器人上面 | Compile and run the program on the robot |
| README | 需要先上电启动舵机之后，后面的行动才可用 | Power the servos first; later moves work only after that |
| `MainActivity` | 打开舵机 / 关闭舵机 | Open / close the servos |
| `MainActivity` | 向前走 | Walk forward |
| `MainActivity` | 注册sensor | Register the sensor callback |
| `MainActivity` | 打开sensor / 关闭sensor | Open / close the sensor |
| layout | 耳朵转动 / 耳朵亮灯 | Rotate the ears / light the ears |
| layout | 显示充电图标 / 隐藏充电图标 | Show / hide the charging icon |
