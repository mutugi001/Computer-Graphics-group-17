from PIL import Image

def mandelbrot(width, height, max_iter):
    # Define the region of the complex plane to visualize
    xmin, xmax = -2.5, 1.5
    ymin, ymax = -2.0, 2.0
    
    # Create a new grayscale image ("L" mode)
    image = Image.new("L", (width, height))
    pixels = image.load()

    for x in range(width):
        for y in range(height):
            # Map pixel position to a point in the complex plane
            a = xmin + (x / width) * (xmax - xmin)
            b = ymin + (y / height) * (ymax - ymin)
            c = complex(a, b)
            z = 0
            iter_count = 0
            
            # Mandelbrot iteration
            while abs(z) <= 2 and iter_count < max_iter:
                z = z * z + c
                iter_count += 1

            # Map the iteration count to a grayscale value (0-255)
            # Points inside the Mandelbrot set will be black if iter_count == max_iter
            color = int(255 * iter_count / max_iter)
            pixels[x, y] = color

    return image

if __name__ == "__main__":
    # Define image dimensions and maximum iterations
    width = 800
    height = 800
    max_iter = 100

    # Generate the Mandelbrot image and save it
    mandelbrot_image = mandelbrot(width, height, max_iter)
    mandelbrot_image.save("mandelbrot.png")
    mandelbrot_image.show()
