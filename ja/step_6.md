## Dropping blocks as you walk

今度はブロックを落とす方法を学びましょう。移動するとブロックを落とすようにしましょう。

次のコードは、歩くとどこにでも花を落とします：

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

前方に歩いて、あなたが後ろに残した花を見てください。

![](images/mcpi-flowers.png)

whileループを使用してから、これは永遠に続くでしょう。 止めるには、PythonウィンドウでCtrl + Cキーを押します.

空を飛んで、あなたが空に残す花を見てみましょう：

![](images/mcpi-flowers-sky.png)

プレイヤーが芝生の上を歩いているときに花を落としたければどうでしょうか？ getBlockを使用して、ブロックのタイプを調べることができます。

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
this_block = mc.getBlock(x, y, z)  # block ID
print(this_block)
```

これはあなたが立っているブロックの位置を示します（これは0になります - エアブロック）。 私たちがどんなタイプのブロックを立てているのかを知りたい。 このために、y値から1を減算し、getBlock（）を使用して、どのタイプのブロックが立っているかを判別します。

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
block_beneath = mc.getBlock(x, y-1, z)  # block ID
print(block_beneath)
```

これは、プレイヤーが立っているブロックのIDを示します。

現在立っているもののブロックIDを出力するループを実行して、これをテストします。

```python
while True:
    x, y, z = mc.player.getPos()
    block_beneath = mc.getBlock(x, y-1, z)
    print(block_beneath)
```

![](images/blockbeneath.gif)

if文を使用して、花を植えるかどうかを選択できます。

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

次は、すでに芝生でない場合、立っているタイルを草に変えることができます。

```python
if block_beneath == grass:
    mc.setBlock(x, y, z, flower)
else:
    mc.setBlock(x, y-1, z, grass)
```

今私達は前方に歩くことができ、私達が草の上を歩くと、私たちは花を残すでしょう。 次のブロックが草でない場合、それは草に変わります。 私たちが向きを変えて歩いていくと、私たちの後ろに花が残っています。
![](images/mcpi-flowers-grass.png)

