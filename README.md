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


## Image border

from PIL import Image, ImageOps
img = Image.open('original-image.png')
img_with_border = ImageOps.expand(img,border=300,fill='black')
img_with_border.save('imaged-with-border.png')

https://stackoverflow.com/questions/11142851/adding-borders-to-an-image-using-python


# Outline 

def stroke(origin_image, threshold, stroke_size, colors):
    img = np.array(origin_image)
    h, w, _ = img.shape
    padding = stroke_size + 50
    alpha = img[:,:,3]
    rgb_img = img[:,:,0:3]
    bigger_img = cv2.copyMakeBorder(rgb_img, padding, padding, padding, padding, 
                                        cv2.BORDER_CONSTANT, value=(0, 0, 0, 0))
    alpha = cv2.copyMakeBorder(alpha, padding, padding, padding, padding, cv2.BORDER_CONSTANT, value=0)
    bigger_img = cv2.merge((bigger_img, alpha))
    h, w, _ = bigger_img.shape
    
    _, alpha_without_shadow = cv2.threshold(alpha, threshold, 255, cv2.THRESH_BINARY)  # threshold=0 in photoshop
    alpha_without_shadow = 255 - alpha_without_shadow
    dist = cv2.distanceTransform(alpha_without_shadow, cv2.DIST_L2, cv2.DIST_MASK_3)  # dist l1 : L1 , dist l2 : l2
    stroked = change_matrix(dist, stroke_size)
    stroke_alpha = (stroked * 255).astype(np.uint8)

    stroke_b = np.full((h, w), colors[0][2], np.uint8)
    stroke_g = np.full((h, w), colors[0][1], np.uint8)
    stroke_r = np.full((h, w), colors[0][0], np.uint8)

    stroke = cv2.merge((stroke_b, stroke_g, stroke_r, stroke_alpha))
    stroke = cv2pil(stroke)
    bigger_img = cv2pil(bigger_img)
    result = Image.alpha_composite(stroke, bigger_img)
    return result

def change_matrix(input_mat, stroke_size):
    stroke_size = stroke_size - 1
    mat = np.ones(input_mat.shape)
    check_size = stroke_size + 1.0
    mat[input_mat > check_size] = 0
    border = (input_mat > stroke_size) & (input_mat <= check_size)
    mat[border] = 1.0 - (input_mat[border] - stroke_size)
    return mat

def cv2pil(cv_img):
    cv_img = cv2.cvtColor(cv_img, cv2.COLOR_BGRA2RGBA)
    pil_img = Image.fromarray(cv_img.astype("uint8"))
    return pil_img
    
    
output = stroke(test_image, threshold=0, stroke_size=10, colors=((0,0,0),))

# Fillig image with color
https://stackoverflow.com/questions/46725396/python-pil-fill-an-image-with-a-color-outline


import os.path
import sys

from PIL import Image, ImageDraw, PILLOW_VERSION


def get_img_dir() -> str:
    pkg_dir = os.path.dirname(__file__)
    img_dir = os.path.join(pkg_dir, '..', '..', 'img')
    return img_dir


if __name__ == '__main__':
    input_img = os.path.join(get_img_dir(), 'star_transparent.png')
    image = Image.open(input_img)
    width, height = image.size
    center = (int(0.5 * width), int(0.5 * height))
    yellow = (255, 255, 0, 255)
    ImageDraw.floodfill(image, xy=center, value=yellow)
    output_img = os.path.join(get_img_dir(), 'star_yellow.png')
    image.save(output_img)

    print('Using Python version {}'.format(sys.version))
    print('Using Pillow version {}'.format(PILLOW_VERSION))
    
    
 # AddingBorder
 
 https://pythoninformer.com/python-libraries/pillow/image-manipulation-recipes/
    from PIL import Image

    im = Image.open('lioness-crop.jpg')
    border_im = Image.new('RGB', (im.width+20, im.height+20), 'yellow')
    border_im.paste(im, (10, 10))
    border_im.save('lioness-border.jpg')
