For Setting up the project
1. Add plugin > ionic cordova plugin add cordova-plugin-camera
2. npm install --save @ionic-native/camera
3. Add Camera provider in app.module  import { Camera } from '@ionic-native/camera';
4. Add method for taking photos

import { Camera, CameraOptions } from '@ionic-native/camera';

images: Array<{src: String}>;

constructor(public navCtrl: NavController, private camera: Camera) {
  this.images = [];
}
takePhoto() {
    const options: CameraOptions = {
      quality: 80,
      destinationType: this.camera.DestinationType.DATA_URL,
      sourceType: this.camera.PictureSourceType.CAMERA,
      allowEdit: false,
      encodingType: this.camera.EncodingType.JPEG,
      saveToPhotoAlbum: false
    }
    this.camera.getPicture(options).then((imageData) => {
      // imageData is either a base64 encoded string or a file URI
      // If it's base64:
      let base64Image = 'data:image/jpeg;base64,' + imageData;
      this.images.unshift({
        src: base64Image
      })
    }, (err) => {
      // Handle error
    });
  }
