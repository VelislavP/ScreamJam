How to use the AudioManager:


1. Add a new ```Sound``` element to the Sounds array
2. Give it a clip
3. If you want to use the Advanced Settings first select `Advanced Mode` otherwise they will be set to default
4. If you want a sound to have a different `Audio Mixer Group` from `Master` you have to set one to the sound. The default is `Master`
5. Don’t forget to click the `Save` button at the bottom when you are done with adding a `Sound`
This will create a `soundsEnum.cs` in the Audio folder, which you can use to select a sound to play in your code

![Screenshot 2021-10-20 195312](https://user-images.githubusercontent.com/43537072/138137258-4b1f505f-bd81-4f78-b221-0ebc5ec122c4.png)
	
This happens with:

```FindObjectOfType<AudioManager>().PlayFromAudioManager(soundsEnum.<name of the sound you added>);```

This is used only for sounds that do not require `3D Spatial Blend`

For sounds that require `3D Spatial Blend` you must do the following:

To the script of the object that you want to emit the sound add an `AudioSource` variable(this is done for every different sound that you want that object to play)

`AudioSource myAudioSource;`

Then you must add this if the object’s script is disabled in the beginning of the game: 

  ```
  void OnEnable()
  {
      SceneManager.sceneLoaded += OnSceneLoaded;
  }

  private void OnSceneLoaded(Scene scene, LoadSceneMode mode)
  {
        myAudioSource = FindObjectOfType<AudioManager>().AddAudioSourceWithSound(gameObject, soundsEnum.UI1);
  }
  ```
  Otherwise you can do:

  ```
  myAudioSource = FindObjectOfType<AudioManager>().AddAudioSourceWithSound(gameObject, soundsEnum.UI1);
  ```
in the Awake()
	
Then to play the sound when needed add the following:

```FindObjectOfType<AudioManager>().PlayFromGameObject(myAudioSource);```
		
```myAudioSource.Play()``` works too, but please use the one above so we can easily add more functionallyty to the method if needed.
