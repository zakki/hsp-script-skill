# HSP Ray Tracing Demo

標準 HSP3 のウィンドウスクリプトで動く、CPU レイトレーシングのデモです。

## 実行

HSP Script Editor で `raytracing.hsp` を開いて実行してください。

OpenHSP をローカルで使う場合のコンパイル例:

```sh
$OPENHSP_ROOT/hspcmp --compath=$OPENHSP_ROOT/common/ -i -o/tmp/raytracing_obj raytracing.hsp
```

## 操作

- `Space`: 自動回転のオン/オフ
- `R`: 再描画
- `Esc`: 終了

低解像度で球・市松模様の床・影・1 回反射を計算し、拡大して表示します。
