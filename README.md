#Tricolor Qr_Code - code
import qrcode
from PIL import Image, ImageDraw

# --- Step 1: Create the tricolor background ---
width = 600
height = 900   # Height split into 3 equal parts
bg = Image.new("RGB", (width, height), "white")
draw = ImageDraw.Draw(bg)

# Colors of the Indian flag
saffron = (255, 153, 51)
white   = (255, 255, 255)
green   = (19, 136, 8)

# Draw rectangles
draw.rectangle([0, 0, width, height//3], fill=saffron)
draw.rectangle([0, height//3, width, 2*height//3], fill=white)
draw.rectangle([0, 2*height//3, width, height], fill=green)

# --- Step 2: Create the QR code ---
qr = qrcode.QRCode(
    version=3,
    error_correction=qrcode.constants.ERROR_CORRECT_H,
    box_size=10,
    border=4,
)

qr.add_data("https://www.linkedin.com/in/yuvraj-singh-parihar-0a9157339")
qr.make(fit=True)

qr_img = qr.make_image(fill_color="navy", back_color="white").convert("RGBA")

# --- Step 3: Resize QR and paste it onto the tricolor ---
qr_img = qr_img.resize((500, 500))  # Adjust size as needed
qr_x = (width - 500) // 2
qr_y = (height - 500) // 2

bg.paste(qr_img, (qr_x, qr_y), qr_img)

# --- Step 4: Save final output ---
bg.save("tricolor_qr.png")
