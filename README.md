## Koushi Chutoh Kyoiku School 
------

<center>

## 生成AIを副操縦士としたPythonプログラミングの超入門 <!-- omit in toc -->

### 新潟市立高志中等教育学校　 <!-- omit in toc -->
#### 2025/2/15(土)  9:30 - 10:45, 11:00  <!-- omit in toc -->
#### 講師：　開志専門職大学　情報学部　堀川 桂太郎 <!-- omit in toc -->
</center>

----

### 概要：

- 従来のプログラミング入門とは一線を画した全く新しい、
- 挫折しないプログラミング入門の導入編
- PokeLLMONの実況ナレーションの紹介から、生成AIの実力、世界観を知ってもらう
- 自分達の仕事・生活に及ぼすインパクトを感じてもらう

----

### 本日のお品書き：メニュー  <!-- omit in toc -->

1. プログラミング：　楽しむ、ご利益
2. さっそくやってみよう
3. 図形を描く
4. 2Dを3Dへ
5. 銀河系を描く
6. シューティングゲーム？
7. 生成AIとの関係、立ち位置
8. 向いている? 向いていない? これからどうする？

----
### 準備体操

- Webブラウザ（Chrome,Safari, Edge,Firefox ・‥）を起動
- Googleアカウントでログイン:　URL： https://www.google.co.jp/
- Colaboratoryに入る: URL: https://colab.research.google.com/
- 「ノートブックを新規作成」
- 「+ コード」をクリックしてコードの入力状態へ
- 🔷Gemini：「利用可能なAI機能」をつかってコード生成を試す：「コードを生成する」
- 「日本語の文字列を読み上げる発話コードをPythonで作ってください。」

```python
# prompt: 日本語の文字列を読み上げる発話コードをPythonで作ってください。
!pip install gTTS

from gtts import gTTS
from IPython.display import Audio

def speak_japanese(text):
  tts = gTTS(text=text, lang='ja')
  tts.save("speech.mp3")
  return Audio("speech.mp3", autoplay=True)

# Example usage
speak_japanese("憧れてしまったら超えられない")

```
- 実行ボタン（▼）をクリックして動作確認する



----

### 図形を描く

- お題：　ハート型の曲線を描いてみる
- 条件：　一行もコードを書かない
- 生成AIへのお願いメッセージ（プロンプト）を考えてみよう

```
 ハート型を描くPythonコードを教えてください
```

- 生成AIの回答例（時と場合によって変ります）

```python
# prompt: ハート型を描くPythonコードを教えてください
import matplotlib.pyplot as plt
import numpy as np

def heart_curve(t):
  x = 16 * np.sin(t)**3
  y = 13 * np.cos(t) - 5 * np.cos(2*t) - 2 * np.cos(3*t) - np.cos(4*t)
  return x, y

t = np.linspace(0, 2*np.pi, 1000)
x, y = heart_curve(t)

plt.plot(x, y, color='red')
plt.axis('equal')
plt.axis('off')  # 軸を非表示にする
plt.show()

```

![alt text](image.png)

```
 線の太さを太くして、色をピンクで塗りつぶしてください
```

- 生成AIの回答例（時と場合によって変ります）

```python
# prompt: 線の太さを太くして、色をピンクで塗りつぶしてください

import matplotlib.pyplot as plt
import numpy as np


def heart_curve(t):
  x = 16 * np.sin(t)**3
  y = 13 * np.cos(t) - 5 * np.cos(2*t) - 2 * np.cos(3*t) - np.cos(4*t)
  return x, y

t = np.linspace(0, 2*np.pi, 1000)
x, y = heart_curve(t)

plt.plot(x, y, color='red', linewidth=5) # Linewidth increased and color changed to pink
plt.fill(x, y, color='pink') # Filled with pink color
plt.axis('equal')
plt.axis('off')  # 軸を非表示にする
plt.show()

```
![alt text](image-1.png)


```
トランプのスペード型とクラブとダイヤの曲線を描いてください
```

![alt text](image-6.png)

----

### 2Dから3D図形へ

- お題：　ハートを3次元で表現する
- 条件：　一行もコードを書かない
- 生成AIへのお願いメッセージ（プロンプト）を考えてみよう
- 
```
 ハート曲線を3次元表示してください。
 plotlyを使って視点を移動できるようにしてください。
 ハートを7段重ねて表示してください。
 ハート曲線の色は、虹のように七色にしてください。

```

- 生成AIの回答例（時と場合によって変ります）

```python
# prompt:  ハート曲線を3次元表示してください。
#  plotlyを使って視点を移動できるようにしてください。
#  ハートを7段重ねて表示してください。
#  ハート曲線の色は、虹のように七色にしてください。

import plotly.graph_objects as go
import numpy as np

def heart_curve(t):
  x = 16 * np.sin(t)**3
  y = 13 * np.cos(t) - 5 * np.cos(2*t) - 2 * np.cos(3*t) - np.cos(4*t)
  return x, y

colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']
fig = go.Figure()

for i in range(7):
    t = np.linspace(0, 2*np.pi, 1000)
    x, y = heart_curve(t)
    z = np.full_like(x, i) # z座標は段数に対応

    fig.add_trace(go.Scatter3d(x=x, y=y, z=z, mode='lines',
                              line=dict(width=10, color=colors[i % len(colors)])))

fig.update_layout(scene=dict(
                    xaxis_visible=False,
                    yaxis_visible=False,
                    zaxis_visible=False,
                    aspectmode='data'
                ),
                title='3D Heart Curve',
                showlegend=False)

fig.show()

```

![alt text](image-2.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# 媒介変数 t の範囲設定
t = np.linspace(0, 2 * np.pi, 1000)

# ハート曲線の方程式
x = 16 * np.sin(t)**3
y = 13 * np.cos(t) - 5 * np.cos(2 * t) - 2 * np.cos(3 * t) - np.cos(4 * t)
y *= -1

# 3Dプロット空間
fig = plt.figure(figsize=(7, 7))  # 図形のサイズ調整
ax = fig.add_subplot(111, projection='3d')

# 7色 (レインボーカラー)
colors = ['red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet']

# ハート曲線を7回重ねる
for i, color in enumerate(colors):
    z = np.full_like(t, i)  # z軸方向にそれぞれの層を配置
    ax.plot(x, y, z, color=color, linewidth=8, label=f'Layer {i+1}')

# グラフの装飾
ax.set_title("3D Heart Curve with 7 Layers", fontsize=16)
ax.set_xlabel("X-axis")
ax.set_ylabel("Y-axis")
ax.set_zlabel("Z-axis")
ax.legend(loc='upper right')
ax.grid(False)

ax.view_init(elev=40, azim=55)

plt.show()
```

![alt text](image-3.png)


---
###  銀河系を描く

- お題：　銀河系のイメージ図を描く
- 条件：　一行もコードを書かない
- 生成AIへのお願いメッセージ（プロンプト）を考えてみよう

```

宇宙の銀河系の星々を擬似的に生成してください。
背景は暗闇で、星の色や大きさはランダムに発色させてください。
銀河系全体は、腕が10本ある渦巻のような形を描写してください。
PythonコードとPlotlyを用いて、インタラクティブな3次元空間にプロットしてください。
```

- 生成AIの回答例（時と場合によって変ります）

```python

import numpy as np
import plotly.graph_objects as go

# 星の数を設定
num_stars = 5000

# 銀河系の腕の数
num_arms = 10

# 星の位置を生成
theta = np.random.uniform(0, 2 * np.pi, num_stars)
radius = np.random.uniform(0, 100, num_stars)  # 半径をランダムに設定
arm_offset = np.random.uniform(0, 2 * np.pi / num_arms, num_stars) # 各腕のオフセット

x = radius * np.cos(theta + arm_offset * num_arms)
y = radius * np.sin(theta + arm_offset * num_arms)
z = np.random.normal(0, 10, num_stars) # z軸方向の位置を正規分布で生成


# 星の色と大きさをランダムに設定
colors = np.random.rand(num_stars, 3) # RGB値で色を設定
sizes = np.random.uniform(1, 5, num_stars)  # 大きさをランダムに設定

# Plotlyで3D散布図を作成
fig = go.Figure()

fig.add_trace(go.Scatter3d(
    x=x,
    y=y,
    z=z,
    mode='markers',
    marker=dict(
        size=sizes,
        color=colors,
        opacity=0.8  # 透明度を設定
    )
))

# レイアウトを設定
fig.update_layout(
    title='Simulated Galaxy',
    scene=dict(
        xaxis_visible=False,
        yaxis_visible=False,
        zaxis_visible=False,
        bgcolor='black'  # 背景色を黒に設定
    )
)

fig.show()
```

![alt text](image-4.png)

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# 銀河系の星を擬似生成
def generate_galaxy(num_stars=10000, disk_radius=15, disk_thickness=1.0):
    """
    銀河系の星を生成
    Parameters:
        num_stars (int): 星の数
        disk_radius (float): 銀河の半径
        disk_thickness (float): 銀河の厚さ
    Returns:
        x, y, z (numpy.ndarray): 各星の3次元座標
    """
    # 星の距離 (指数分布で中心に集中)
    r = np.random.exponential(scale=disk_radius / 3, size=num_stars)
    r = r[r < disk_radius]  # 銀河系の半径を超える星を除外
    theta = np.random.uniform(0, 2 * np.pi, len(r))
    z = np.random.normal(0, disk_thickness, len(r))
    x = r * np.cos(theta)
    y = r * np.sin(theta)

    return x, y, z

# 星を生成
num_stars = 10000
x, y, z = generate_galaxy(num_stars)

z_normalized = (z - np.min(z)) / (np.max(z) - np.min(z))

# 色マップ (グラデーション：　青 -> 白 -> 黄色 -> 赤)
colors = plt.cm.coolwarm(z_normalized)

# 3Dプロット
fig = plt.figure(figsize=(7, 7))
ax = fig.add_subplot(111, projection='3d')
scatter = ax.scatter(x, y, z, s=1, c=colors, alpha=0.7)

# 背景色：黒
ax.set_facecolor('black')
fig.patch.set_facecolor('black')

ax.set_xticks([])
ax.set_yticks([])
ax.set_zticks([])
ax.set_xlim([-15, 15])
ax.set_ylim([-15, 15])
ax.set_zlim([-3, 3])
ax.set_box_aspect([1, 1, 0.1])  # 銀河ディスクの形状を反映

ax.set_title("Milky Way Galaxy with Star Colors", color='white', fontsize=12)
plt.show()

```

![alt text](image-5.png)


----

### シューティングゲーム？






-----

### 生成AIとの関係、立ち位置

----

### 向いている? 向いていない? これからどうする？
