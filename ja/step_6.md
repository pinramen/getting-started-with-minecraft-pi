## 歩いてブロックを落とす方法

今度はブロックを落とす方法です。移動する場所を歩いてブロックを落とすようにしましょう。
次のコードは、歩いてどこにでも花を落とします。

```python
from mcpi.minecraft import Minecraft
from time import sleep

mc = Minecraft.create()

flower = 38

while True:
    x, y, z = mc.player.getPos()
    mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

今すぐ前に歩いて、後ろに落とした花を見るために回ってください。

![](images/mcpi-flowers.png)

whileループを使用すると、これはずっと続きます。 止めるには、PythonウィンドウでCtrl + Cキーを押します。

空を飛んで、あなたが空に残す花を見てください。

![](images/mcpi-flowers-sky.png)

プレイヤーが芝生の上を歩いているときに花を落としたければどうすればいいでしょうか？ getBlockを使用してブロックのタイプを調べることができます。

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
this_block = mc.getBlock(x, y, z)  # block ID
print(this_block)
```

これはあなたが立っているブロックの位置を示します（これは0になります - エアブロック）。 私たちがどんなタイプのブロックを立てているのかを知りたいときは、y値から1を減算し、getBlock（）を使用して、どのタイプのブロックが立っているかを判断します。

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
block_beneath = mc.getBlock(x, y-1, z)  # block ID
print(block_beneath)
```
これは、プレイヤーが立っているブロックのIDを示します。
これをテストするには、現在立っているもののブロックIDを出力するループを実行してください。

```python
while True:
    x, y, z = mc.player.getPos()
    block_beneath = mc.getBlock(x, y-1, z)
    print(block_beneath)
```

![](images/blockbeneath.gif)

この文を使用して、花を植えるかどうかを選択できます。

```python
grass = 2
flower = 38

while True:
    x, y, z = mc.player.getPos()  # player position (x, y, z)
    block_beneath = mc.getBlock(x, y-1, z)  # block ID

    if block_beneath == grass:
        mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

次に、立っているブロックが、すでに芝生でない場合は芝生に変えることができます。

```python
if block_beneath == grass:
    mc.setBlock(x, y, z, flower)
else:
    mc.setBlock(x, y-1, z, grass)
```

あなたが前に歩き、あなたが草の上を歩くと、花を落とします。 次のブロックが草でない場合、それは草に変わります。 あなたが向きを変えて歩いていくと、後ろに花が残っています。

![](images/mcpi-flowers-grass.png)

