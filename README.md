# jupyter-enterprise-gateway 安裝過程
## 安裝虛擬環境

*  這裡沒有要求一定要用anaconda/miniconda或virtualenv套件，使用虛擬環境原因除了可以設定自己的使用環境不干擾其他使用環境，之後可以打包成zip檔上傳至YARN讓其他的executor去使用相關的package，我是使用miniconda安裝虛擬環境

    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86.sh
    chmod +x ./Miniconda3-latest-Linux-x86_64.sh
    ./Miniconda3-latest-Linux-x86_64.sh
    source ~/.bashrc
    
    
    
