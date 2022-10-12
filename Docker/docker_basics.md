## How to export/import docker images from a local repo
___
</br>

- List the locally available images:  

  ```
  docker images
  ```

- Export the image as a .tar file: 

  ```
  docker save -o ~/Docker/myimage.tar <image_id>
  ```

- Import an image from a .tar file:

  ```
  docker load -i myimage.tar  
  ```  