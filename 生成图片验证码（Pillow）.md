Pillow是从PIL派生出来的一个Python第三方图像处理库，功能非常强大。运用Pillow可以很方便的完成各种图片处理的操作。通过写一段生成图片验证码的代码可以对Pillow有一个初步的认识。
Pillow的安装：
	python -m pip install pillow
```python
from random import randint, choice
from PIL import Image, ImageDraw, ImageFilter, ImageFont


def char_generator():
    """随机生成验证码"""
    char_list = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    char = char_list[randint(0, 61)]
    return char


def random_color1():
    """随机颜色1（用于填充字体）"""
    return randint(10, 80), randint(10, 80), randint(10, 80)


def random_color2():
    """随即颜色2（用于填充背景）"""
    return randint(100, 255), randint(100, 255), randint(100, 255)


def img_code():
    im = Image.new('RGB', (142, 50))  # 新建一个图片
    draw = ImageDraw.Draw(im) # 构造一个ImageDraw对象
    for x in range(142):
        for y in range(50):
            draw.point((x, y), fill=random_color2()) # 对每个像素点进行填充
    font = ImageFont.truetype('fonts/%d.ttf' % randint(1, 10), 32) # 设置字体
    filename = ''
    for j in range(4):  # 画上字符
        code_str = char_generator()
        draw.text((10 + j * 35, 6), code_str, font=font, fill=random_color1()) 
        filename += code_str
    im = im.filter(ImageFilter.BLUR)  # 模糊化
    im.save('%s.jpg' % filename, 'jpeg')  # 保存图片


if __name__ == '__main__':
    img_code()

```
生成的图片验证码：
![这里写图片描述](https://img-blog.csdn.net/20180420203810557?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ZpcmVfRmFuZzIwMDE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) ![这里写图片描述](https://img-blog.csdn.net/20180420203818730?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ZpcmVfRmFuZzIwMDE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) ![这里写图片描述](https://img-blog.csdn.net/20180420203826761?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ZpcmVfRmFuZzIwMDE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
