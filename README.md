# Usefull notebook and Snippet
## NFT
https://www.danielhugenroth.com/posts/2020_08_python_drawing/
https://github.com/pygobject/pycairo/tree/master/examples
https://generativeartistry.com/tutorials/
https://github.com/tholman/generative-artistry/


# game of life and pixel generator

https://jakevdp.github.io/blog/2013/08/07/conways-game-of-life/
https://towardsdatascience.com/from-scratch-the-game-of-life-161430453ee3
https://godhalakshmi.medium.com/a-simple-introduction-to-the-world-of-fractals-using-python-c8cb859bfd6d
https://www.startprism.com/how-to-paint-like-piet-mondrian-with-python/

# recursive generative art
https://franklin.dyer.me/post/169
https://opensourcelibs.com/lib/anaulin-generative-art
# pycairo
https://engineeredjoy.com/blog/generative-art-python/
https://devpost.com/software/generative-art-z7swoc
http://makeyourownalgorithmicart.blogspot.com/2019/


# Code
https://gist.github.com/yudevan/ad58d185bd5723719b30c0921a9c9eb7
https://githubhelp.com/JakobGlock/Generative-Art


# Background effect
https://engineeredjoy.com/blog/perlin-noise/
https://engineeredjoy.com/blog/pycairo-alpha-mask-group/

# Outline stroke 
https://stackoverflow.com/questions/61405583/how-can-i-add-an-outline-stroke-border-to-a-png-image-with-pillow-library-in-pyt

https://jdhao.github.io/2020/08/18/pillow_create_text_outline/


# Resize
## Ratio 
https://jdhao.github.io/2017/11/06/resize-image-to-square-with-padding/
https://scikit-image.org/docs/dev/auto_examples/edges/plot_contours.html#sphx-glr-auto-examples-edges-plot-contours-py

https://stackoverflow.com/questions/10965417/how-to-convert-a-numpy-array-to-pil-image-applying-matplotlib-colormap

https://gist.github.com/namieluss/a440061734075d929f0c6b9f6bd919c7
from PIL import Image, ImageOps

# open image
img = Image.open("test_image.jpg")

# border color
color = "green"

# top, right, bottom, left
border = (20, 10, 20, 10)

new_img = ImageOps.expand(img, border=border, fill=color)

# save new image
new_img.save("test_image_result.jpg")

# show new bordered image in preview
new_img.show()
