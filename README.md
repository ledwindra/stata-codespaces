# Steps

1. Install [Visual Studio Code](https://code.visualstudio.com/Download)

2. Create your [codespaces](https://github.com/codespaces) and choose VS Code to open your codespaces

<img width="1293" alt="image" src="https://user-images.githubusercontent.com/39021609/130315231-9b42421c-16ed-439c-b704-43ca88f91c39.png">

3. Create a Python virtual environment (Python is already pre-installed) and install required packages

```bash
sudo apt-get install python3.8-venv
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
python -m stata_kernel.install
jupyter labextension install jupyterlab-stata-highlight
```

4. Install [Stata for Linux](https://download.stata.com/download/linux64_15/). Follow their instruction on your terminal. You need to input serial number, code, and authorization
  - In `tar -zxf /home/you/Downloads/Stata15Linux64.tar.gz` part, change `/home/you/Downloads/` to your directory
  - In my case, it's `/workspaces/stata-codespaces/`

5. After installing Stata, install this Ubuntu package because otherwise it will cause an error when invoking your Stata. Just type yes when you're prompted to

```bash
# https://askubuntu.com/questions/895897/error-while-loading-shared-libraries-libpng12-so-0
wget http://archive.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng_1.2.54.orig.tar.xz
tar xvf  libpng_1.2.54.orig.tar.xz 
cd libpng-1.2.54
./autogen.sh
./configure
make -j8 
sudo make install
sudo ldconfig
sudo apt-get install libtool autoconf build-essential pkg-config automake tcsh
```

6. Exit from root by typing `exit` and then you're back to virtual environment

<img width="627" alt="image" src="https://user-images.githubusercontent.com/39021609/130315818-941fbdfd-fe1e-48ce-acc4-1a346c501438.png">

7. Add Stata to your $PATH. Note that if you are using Stata MP, for example, then you need to add change `stata15` to `stata15-mp`; same thing if you're using Stata SE
  - Type `nano ~/.bashrc` on your terminal, it will prompt you to a Nano text editor
  - Scroll to bottom, and insert the following
  ```bash
  # stata path
  export PATH="/usr/local/stata15:$PATH"
  ```
  - Type `source ~/.bashrc`
  - You will be exited from the virtual environment, but no worries, just type `source .venv/bin/activate`

8. You should by now be able to invoke Stata by typing `stata` on terminal

<img width="754" alt="image" src="https://user-images.githubusercontent.com/39021609/130316076-8c126edb-dded-4f98-95c4-a02f243ff25a.png">

9. Almost there! You need to change `stata_kernel` configuration a little bit typing `nano ~/.stata_kernel.conf`. Refer to this [page](https://kylebarron.dev/stata_kernel/using_stata_kernel/configuration/) on `General Settings` - `stata_path` section

<img width="802" alt="image" src="https://user-images.githubusercontent.com/39021609/130316290-dc8fa744-19a1-48dc-bc7d-08b646f28428.png">

10. You're now able to run Stata kernel on Jupyter Notebook using GitHub Codespaces by typing `jupyter notebook` on terminal. Just click open in browser when you're prompted to. Also, you need to input the token. See the censored the part below, that's the token that you're going to use

<img width="1160" alt="image" src="https://user-images.githubusercontent.com/39021609/130316370-c1561bff-6eb4-425e-98ff-b71a27af8aaa.png">

11. Create a new file and choose Stata kernel

<img width="332" alt="image" src="https://user-images.githubusercontent.com/39021609/130316420-5f88d046-ea50-4da2-a5d7-2d6502a4f5e6.png">

12. That's it, enjoy!

<img width="587" alt="image" src="https://user-images.githubusercontent.com/39021609/130316450-f17ef11e-1fb5-4acc-812d-909f74215293.png">

# Miscellaneous
- Let me know if you have any questions by submitting issues [here](https://github.com/ledwindra/stata-codespaces/issues)
