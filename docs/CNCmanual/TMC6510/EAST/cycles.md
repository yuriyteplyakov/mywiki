## Для канала 2

### Упрощенные циклы продольного и поперечного точения

``` gcode

N10 (CHERN PROHOD)
G0 G40 G54 G90 G95
(G95 - подача на оборот)
G53 X0 Z-500 (машинные координаты)
T0101
GETD S = 4 (захват левого токарного шпинделя)
G109 C0 (переключение шпинделя в режим скорости)
M3 G97 S360 F0.3
(G96 - отключение постоянной скорости резания на данном оборудовании не работает)
X112 Z20 (подьезд на безопасном расстоянии от детали)
Z3 M8
G81 X60 Z0.1 (упрощенный цикл поперечного точения)
;G0 Z1 (G0 его отменяет, но можно и без этого, если дальше следует другой цикл)
G80 X106 Z-13 (цикл продольного точения)
X104 (здесь указываются промежуточные диаметры, вместо глубины резания)
G0 X99.6
G1 Z0
Z-1.6 X104 (предварительная фаска)
G0 G53 X0 Z-500 M5 M9
M1
```

### Цикл внутреннего растачивания со ступенькой

``` gcode

X60 Z20 M8
(Упрощенный цикл)
G81 X106 Z0
G0 X66 Z2
G80 X69 Z-2.1
X72
X74
(FINISH)
#1 = 0.4 (RAD SKRUGL)
G0 G41 X[75.2 + 2 * #1]
G1 Z0 F0.3
G2 X75.2 Z[-#1] R#1 F0.05
G1 Z-2.125 F0.2 (D75 CHIST)
X66.06 Z[-2.125 - #1] R#1 F0.05
G0 G40 X60
Z20
G53 X0 Z-500 M5 M9
```