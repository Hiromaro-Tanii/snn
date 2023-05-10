# snn

dem_autoencoder_segmentation.py

 image = image.reshape(4096,10)で実行↓
 
 
network.py  276行目でエラー発生
「index 10 is out of bounds for dimension 2 with size 10」
↑回避した


dem_autoencoder_segmentation.py のいじったところ

35:image = image.reshape(4096,10)→
37:label = label.reshape(4096)→
45:parser.add_argument('--batch', '-b', type=int, default=32)  →default=8
46: parser.add_argument('--epoch', '-e', type=int, default=100)  →default=50
47:parser.add_argument('--time', '-t', type=int, default=101)  →default=10

network.pyのいじったところ

209:def __init__(self, num_time=20, l_tau=0.8, soft=False, rec=False, forget=False, dual=False, power=False, gpu=True,↓
    def __init__(self, num_time=10, l_tau=0.8, soft=False, rec=False, forget=False, dual=False, power=False, gpu=True,

229:self.up_samp = nn.Upsample(scale_factor=2, →self.up_samp = nn.Upsample(scale_factor=8,
 
    
313: out_rec = torch.stack(out_rec,dim=1)  →out_rec = torch.stack(out_rec,dim=1)


network.py  313行目でエラー発生
stack expects each tensor to be equal size, but got [8, 1, 64, 64] at entry 0 and [8, 1, 1024, 1024] at entry 1
tensorを一致させないといけない。

