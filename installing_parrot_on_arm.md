# Installation steps for apple silicon

From colings86:

```
brew install python@3.8
brew install portaudio
brew install six
brew install libsndfile
git clone https://github.com/chaosparrot/parrot.py.git
cd parrot.py
pip install -r requirements-posix.txt
export CPATH=/opt/homebrew/include                         
export LIBRARY_PATH=/opt/homebrew/lib
export DYLD_LIBRARY_PATH="/opt/homebrew/lib:$DYLD_LIBRARY_PATH"
export PATH=$PATH:/opt/homebrew/Cellar/libsndfile/1.1.0/bin
export PATH="/opt/homebrew/opt/python@3.8/libexec/bin:$PATH"
python settings.py
```

At this point, I got a symbol error when I ran `python3.8 settings.py` on my M2. I fixed that by following `https://stackoverflow.com/questions/33513522/when-installing-pyaudio-pip-cannot-find-portaudio-h-in-usr-local-include`. In particular, I uninstalled pyaudio, and then reinstalled it by doing

    ```
    pip3.8 install --global-option='build_ext' --global-option='-I/opt/homebrew/Cellar/portaudio/19.7.0/include/' --global-option='-L/opt/homebrew/Cellar/portaudio/19.7.0/lib' pyaudio
    ```

I used those paths because my `brew info portaudio` returned `/opt/homebrew/Cellar/portaudio/19.7.0/include/`. That is, we want to use the paths `<result from brew info portaudio>/include` and `<result from brew info portaudio>/lib`.
