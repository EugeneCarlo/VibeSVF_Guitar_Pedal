# VibeFilter — Hybrid Effects Pedal (State Variable Filter) with Open Source Code

---

The project is fully open source: you can replicate the circuit, order PCBs, build the pedal, and modify the firmware to suit your needs.
![VibeFilter](https://cs19.pikabu.ru/s/2026/03/01/17/ktbuwqn2_lg.png)

## Architecture

- Analog section: State Variable Filter (SVF) based on LM13700.
- Digital control: Arduino Nano.

## Specifications

- Power supply: single-polarity 9–12 V.
- Number of analog parameters: 2.
- Number of digital parameters: 3.
- Controls: 2 buttons, 2 bi‑color LEDs.
- True‑bypass (relay).

## Operating Modes

The current firmware offers two main modes, each with two sub‑modes:

**Envelope:**
- Trig (one‑shot trigger)
- Gate (hold).

**LFO (Low‑Frequency Oscillator):**
- Tap‑Tempo (continuous operation)
- Gated (triggered by press).

## Controls

### Potentiometers (Analog)

- **FREQ** – base filter frequency.
- **RES** – filter resonance (Q factor).

### Potentiometers (Digital)

- **Attack/Speed**
  - in Envelope mode: sets attack time.
  - in LFO mode: modulation speed (when tap‑tempo is not used).

- **Decay/Wave**
  - in Envelope mode: sets decay time.
  - in LFO mode: selects waveform.

- **Depth** – effect depth (0–255).

### Buttons

#### Bypass (D5)
- Short press: toggles effect on/off (relay).
- Hold (2 sec): switches sub‑mode.
  - (Trig/Gate in Envelope mode)
  - (Tap Tempo/Gated in LFO mode)
- Hold (6 sec): enables/disables external input processing on A7.  
  Used as an additional trigger/gate source for the envelope and in LFO random mode.

#### Tap/Trigger (D9)
- in Envelope mode (Trig): triggers the envelope.
- in Envelope mode (Gate): holds the envelope.
- in LFO mode (Tap Tempo): sets the tempo.
- in LFO mode (Gated): starts the LFO.

## Mode Selection

To switch the main mode, press and hold both buttons (Bypass and Tap) for about 1 second.  
The Bypass LED color changes:
- Red (Envelope)
- Green (LFO)

### Envelope Mode

- **Trig (trigger):** the envelope fires once when Tap is pressed or when a signal is received on input A7 (if external input is enabled).  
  Envelope shape is attack/decay (AD).  
  Attack and Decay are adjusted with the corresponding potentiometers.  
  Depth sets the maximum level.

- **Gate (hold):** the envelope rises to maximum as long as Tap is held or the signal on A7 is active (if external input is enabled).  
  The decay starts after release.  
  Attack and Decay are adjusted with the corresponding potentiometers.  
  Depth sets the maximum level.

### LFO Mode

- **Tap Tempo:** the LFO runs continuously.  
  Speed can be set with the Attack/Speed potentiometer (manual mode) or by tapping Tap twice at the desired interval;  
  after that, the Speed knob no longer controls the speed (tap‑tempo is active).  
  To return to manual control, simply turn the Speed knob.

- **Gated:** the LFO stays silent until Tap is pressed.  
  When pressed, the LFO starts from the beginning of its waveform and runs as long as the button is held.

#### LFO Waveform

The waveform is selected with the Wave knob:

1 – rising sawtooth  
2 – triangle  
3 – falling sawtooth  
4 – 50% square  
5 – random value (updated every period)

## External Trigger

Enable/disable external input processing in random mode.  
Hold the Bypass button for 6 seconds.  
When toggled, the Tap LED blinks twice dimly.

## Settings Saving

All settings (effect state, selected mode, sub‑modes, manual/automatic LFO speed mode, tap‑tempo interval, external input status) are automatically saved to EEPROM 2 seconds after the last change.


# VibeFilter — Гибридная педаль эффектов (State Variable Filter) с открытым исходным кодом

---

Проект полностью открыт: вы можете повторить схемотехнику, заказать платы, собрать педаль и модифицировать прошивку под свои задачи.

## Архитектура

- Аналоговая часть: State Variable Filter (SVF) на LM13700.
- Цифровое управление: Arduino Nano.

## Спецификация

- Питание: однополярное 9–12 В.
- Количество аналоговых параметров: 2.
- Количество цифровых параметров: 3.
- Органы управления: 2 кнопки, 2 двухцветных светодиода.
- True-bypass (реле).

## Режимы работы

В текущей прошивке доступно два основных режима, каждый из которых имеет два подрежима:

**Envelope (огибающая):**
- Trig (однократный запуск)
- Gate (удержание).

**LFO (низкочастотный генератор):**
- Tap-Tempo (непрерывная работа)
- Gated (запуск по нажатию).

## Органы управления

### Потенциометры (аналоговые)

- **FREQ** – базовая частота фильтра.
- **RES** – резонанс (добротность) фильтра.

### Потенциометры (цифровые)

- **Attack/Speed**
  - в режиме Envelope задаёт время атаки.
  - в режиме LFO – скорость модуляции (если не используется tap-tempo).

- **Decay/Wave**
  - в режиме Envelope задаёт время спада.
  - в режиме LFO задает форму волны.

- **Depth** – глубина эффекта (0–255).

### Кнопки

#### Bypass (D5)
- Короткое нажатие включает/выключает эффект (реле).
- При удержании (2 сек) переключает подрежим.
  - (Trig/Gate в режиме Envelope)
  - (Tap Tempo/Gated в режиме LFO)
- При удержании (6 сек) включает/выключает обработку внешнего входа A7.  
  Используется как дополнительный источник триггера/гейта для огибающей и рандом режиме лфо.

#### Tap/Trigger (D9)
- в режиме Envelope (Trig) запускает огибающую.
- в режиме Envelope (Gate) удерживает огибающую.
- в режиме LFO (Tap Tempo) служит для задания темпа.
- в режиме LFO (Gated) запускает LFO.

## Управление режимами

Для смены основного режима одновременно удерживайте обе кнопки (Bypass и Tap) около 1 секунды.  
Цвет светодиода Bypass изменится:
- Красный (Envelope)
- Зеленый (LFO)

### Режим Envelope

- **Trig (триггерный):** огибающая запускается однократно по нажатию Tap или по сигналу на входе A7 (если внешний вход включён).  
  Форма огибающей – атака/спад (AD).  
  Attack и Decay регулируются соответствующими потенциометрами.  
  Depth задаёт максимальный уровень.

- **Gate (удержание):** огибающая поднимается до максимума, пока удерживается кнопка Tap или активен сигнал на A7 (если внешний вход включён).  
  После отпускания начинается спад.  
  Attack и Decay регулируются соответствующими потенциометрами.  
  Depth задаёт максимальный уровень.

### Режим LFO

- **Tap Tempo:** LFO работает постоянно.  
  Скорость можно задать потенциометром Attack/Speed (в ручном режиме) либо нажать Tap дважды с нужным интервалом,  
  после этого ручка Speed автоматически перестаёт управлять скоростью (активируется tap-tempo).  
  Чтобы вернуть ручное управление, просто поверните ручку Speed.

- **Gated:** LFO молчит, пока не нажата кнопка Tap.  
  При нажатии LFO запускается с начала формы и работает, пока кнопка удерживается.

#### Форма волны LFO

Форма волны выбирается ручкой Wave:

1 – восходящая пила  
2 – треугольник  
3 – нисходящая пила  
4 – меандр 50%  
5 – псевдослучайное значение (обновляется каждый период)

## Внешний триггер

Включение/выключение обработки внешнего входа режиме рандома.  
Удерживайте кнопку Bypass в течении 6 секунд.  
При переключении светодиод Tap дважды тускло мигает.

## Сохранение настроек

Все настройки (состояние эффекта, выбранный режим, подрежимы, ручной/автоматический режим скорости LFO, интервал tap-tempo, статус внешнего входа) автоматически сохраняются в EEPROM через 2 секунды после последнего изменения.
