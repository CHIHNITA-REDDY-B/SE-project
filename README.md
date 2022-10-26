# SE-project
Shivani Clg, [26-10-2022 21:15]
[Forwarded from Nikitha Klu]
from flask import Flask, render_template, request
from werkzeug.utils import secure_filename
from werkzeug import secure_filename, FileStorage
import os, pytesseract
from flask_uploads import UploadSet, configure_uploads, IMAGES
from PIL import Image

project_dir = os.path.dirname(os.path.abspath(file))
app = Flask(name,
            static_url_path='',
            static_folder='static',
            template_folder='template')

photos = UploadSet('photos', IMAGES)  # folder
app.config['DEBUG'] = True
app.config['UPLOAD_FOLDER'] = 'images'


# class for image to text
class GetText(object):
    def init(self, file):
        self.file = pytesseract.image_to_string(Image.open(project_dir + '/images/ ' + file))


app = Flask(name, template_folder='template')


@app.route('/', methods=['GET', 'POST'])
def home():
    if request.method == 'POST':
        if 'photo' not in request.files:
            return 'there is no photo in form'
        name = request.form['img-name'] + '.jpg'
        photo = request.files['photo']
        path = os.path.join(app.config['UPLOAD_FOLDER'], name)
        photo.save(path)
        textObject = GetText(name)
        print('TEXT OBJECT' + textObject.file)
        return textObject.file
    return render_template("conversion.html")


if name == 'main':
    app.run()

Shivani Clg, [26-10-2022 21:15]
<html lang="">
          <head>
                   <meta charset="utf-g">
                   <title>Image to Text</title>
                   <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3xipma34MD+dH/1fQ784/j6cY/iJTQUOhWr7x9JvRxT2MZw1T" crossorigin="anonymous">
          </head>
<body>
<div class='text-center'><br><br>
        <h1>Upload Image Below</h1>
        <form method=POST enctype='multipart/form-data'>
                   <input type='file' class='btn btn-dark' name='photo'><br><br>
                   <input id='input' type='text' class='form-control' placeholder='enter image name...' name='img-name'><br>
                   <input class='btn btn-dark' type='submit'>
          </form>
 </div>
</body>
<style>
      #input{
              margin:auto;
             width: auto;
}
</style>
</html>
