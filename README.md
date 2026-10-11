# ДЗ 1 «Фотолаборатория»

Инструмент командной строки `photolab.py`: цветокоррекция, хромакей, геометрия, контактный лист.

## Установка и самопроверка

```bash
pip install -r requirements.txt
pytest tests -q
```

## Команды, которыми получено всё в `out/`

Свои фотографии лежат в `data/` (фон для хромакея — `data/poster.jpg`).

```bash
python photolab.py gamma data/dark.jpg --gamma 0.5 -o out/dark_g05.jpg --hist out/dark_g05_hist.png
python photolab.py gamma data/dark.jpg --gamma 2.0 -o out/dark_g20.jpg --hist out/dark_g20_hist.png
python photolab.py wb data/bright.jpg --method grey-world -o out/bright_gw.jpg --hist out/bright_gw_hist.png
python photolab.py wb data/bright.jpg --method white-patch -o out/bright_wp.jpg --hist out/bright_wp_hist.png
python photolab.py clahe data/dark.jpg --clip 2 --tiles 8 -o out/dark_clahe.jpg --compare out/dark_cmp.jpg --hist out/dark_clahe_hist.png
python photolab.py chromakey data/object.jpg --bg data/poster.jpg --sample 505,740,30,20 --close 45 -o out/object_on_bg.jpg --mask out/object_mask.png
python photolab.py chromakey data/object.jpg --bg data/poster.jpg --lo 168,70,40 --hi 8,255,255 -o out/object_red_on_bg.jpg --mask out/object_red_mask.png
python photolab.py rotate data/poster.jpg --deg 30 -o out/poster_rot30.jpg
python photolab.py resize data/text.jpg --scale 0.25 --report -o out/text_x025.jpg
python photolab.py rectify data/poster.jpg --corners 907,549,68,666,308,920,569,468 --aspect 1.414 -o out/poster_front.jpg
python photolab.py sheet data/*.jpg out/*.jpg --cols 4 -o out/sheet.jpg   # запускалась последней, когда out/sheet.jpg ещё не было
```

## Проверка на кадрах курса (`out/course/`)

`COURSE` — путь к клону репозитория курса `iu-intro-cv`.

```bash
IU=$COURSE/lectures/L05-filtering/demo/iu-building.jpg
L3=$COURSE/lectures/L03-color-histograms/demo
L4=$COURSE/lectures/L04-geometry/demo
python photolab.py chromakey $L3/ball-lamp.jpg --bg $L4/road-cam.jpg --lo 140,121,40 --hi 168,230,255 -o out/course/ck.jpg --mask out/course/ck_mask.png
python photolab.py resize $IU --scale 0.25 --report -o out/course/small.jpg
python photolab.py rectify $L4/poster-angle.jpg --corners 560,330,1250,220,1290,1010,600,840 --size 640x905 -o out/course/front640.png
```
