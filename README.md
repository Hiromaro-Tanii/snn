# snn


dem_autoencoder_segmentation.pyのいじったところ
35:image = image.reshape(4096,20)→(4096,10)
45:parser.add_argument('--batch', '-b', type=int, default=32)  →default=8
46: parser.add_argument('--epoch', '-e', type=int, default=100)  →default=50
47:parser.add_argument('--time', '-t', type=int, default=101)  →default=10

実行↓
network.py  313行目でエラー発生
「stack expects each tensor to be equal size, but got [8, 1, 64, 64] at entry 0 and [1, 1, 64, 64] at entry 1」
tensorを一致させないといけない。

