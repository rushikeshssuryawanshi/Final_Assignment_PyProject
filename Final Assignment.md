<p style="text-align:center">
    <a href="https://skills.network/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork900-2022-01-01" target="_blank">
    <img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/assets/logos/SN_web_lightmode.png" width="200" alt="Skills Network Logo">
    </a>
</p>


<h1>Extracting and Visualizing Stock Data</h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some stock data, you will then display this data in a graph.


<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
        <li>Define a Function that Makes a Graph</li>
        <li>Question 1: Use yfinance to Extract Stock Data</li>
        <li>Question 2: Use Webscraping to Extract Tesla Revenue Data</li>
        <li>Question 3: Use yfinance to Extract Stock Data</li>
        <li>Question 4: Use Webscraping to Extract GME Revenue Data</li>
        <li>Question 5: Plot Tesla Stock Graph</li>
        <li>Question 6: Plot GameStop Stock Graph</li>
    </ul>
<p>
    Estimated Time Needed: <strong>30 min</strong></p>
</div>

<hr>


***Note***:- If you are working in IBM Cloud Watson Studio, please replace the command for installing nbformat from `!pip install nbformat==4.2.0` to simply `!pip install nbformat`



```python
!pip install yfinance==0.1.67
!mamba install bs4==4.10.0 -yf
!pip install nbformat==4.2.0
```

    Collecting yfinance==0.1.67
      Downloading yfinance-0.1.67-py2.py3-none-any.whl (25 kB)
    Requirement already satisfied: pandas>=0.24 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (1.3.5)
    Requirement already satisfied: numpy>=1.15 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (1.21.6)
    Requirement already satisfied: requests>=2.20 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (2.29.0)
    Collecting multitasking>=0.0.7 (from yfinance==0.1.67)
      Downloading multitasking-0.0.11-py3-none-any.whl (8.5 kB)
    Requirement already satisfied: lxml>=4.5.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (4.9.2)
    Requirement already satisfied: python-dateutil>=2.7.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pandas>=0.24->yfinance==0.1.67) (2.8.2)
    Requirement already satisfied: pytz>=2017.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pandas>=0.24->yfinance==0.1.67) (2023.3)
    Requirement already satisfied: charset-normalizer<4,>=2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (3.1.0)
    Requirement already satisfied: idna<4,>=2.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (3.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (1.26.15)
    Requirement already satisfied: certifi>=2017.4.17 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (2023.5.7)
    Requirement already satisfied: six>=1.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from python-dateutil>=2.7.3->pandas>=0.24->yfinance==0.1.67) (1.16.0)
    Installing collected packages: multitasking, yfinance
    Successfully installed multitasking-0.0.11 yfinance-0.1.67
    
                      __    __    __    __
                     /  \  /  \  /  \  /  \
                    /    \/    \/    \/    \
    ███████████████/  /██/  /██/  /██/  /████████████████████████
                  /  / \   / \   / \   / \  \____
                 /  /   \_/   \_/   \_/   \    o \__,
                / _/                       \_____/  `
                |/
            ███╗   ███╗ █████╗ ███╗   ███╗██████╗  █████╗
            ████╗ ████║██╔══██╗████╗ ████║██╔══██╗██╔══██╗
            ██╔████╔██║███████║██╔████╔██║██████╔╝███████║
            ██║╚██╔╝██║██╔══██║██║╚██╔╝██║██╔══██╗██╔══██║
            ██║ ╚═╝ ██║██║  ██║██║ ╚═╝ ██║██████╔╝██║  ██║
            ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝     ╚═╝╚═════╝ ╚═╝  ╚═╝
    
            mamba (1.4.2) supported by @QuantStack
    
            GitHub:  https://github.com/mamba-org/mamba
            Twitter: https://twitter.com/QuantStack
    
    █████████████████████████████████████████████████████████████
    
    
    Looking for: ['bs4==4.10.0']
    
    [?25l[2K[0G[+] 0.0s
    [2K[1A[2K[0G[+] 0.1s
    pkgs/main/linux-64 [90m━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
    pkgs/main/noarch   [90m╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
    pkgs/r/linux-64    [33m━━━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.1s
    pkgs/r/noarch      [33m━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.1s[2K[1A[2K[1A[2K[1A[2K[1A[2K[0G[+] 0.2s
    pkgs/main/linux-64 [90m━━━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.2s
    pkgs/main/noarch   [90m━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━[0m  57.4kB /  ??.?MB @ 372.5kB/s  0.2s
    pkgs/r/linux-64    [90m━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━━[0m  28.7kB /  ??.?MB @ 186.4kB/s  0.2s
    pkgs/r/noarch      [33m━━━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━[0m   0.0 B /  ??.?MB @  ??.?MB/s  0.2s[2K[1A[2K[1A[2K[1A[2K[1A[2K[0G[+] 0.3s
    pkgs/main/linux-64 [90m━━━━━━━━╸[0m[33m━━━━━━━━━━━━━━━━[0m 491.5kB /  ??.?MB @   1.9MB/s  0.3s
    pkgs/main/noarch   [90m━━━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━[0m 643.1kB /  ??.?MB @   2.4MB/s  0.3s
    pkgs/r/linux-64    [90m━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━[0m 622.6kB /  ??.?MB @   2.4MB/s  0.3s
    pkgs/r/noarch      [90m━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━━[0m 548.9kB /  ??.?MB @   2.1MB/s  0.3s[2K[1A[2K[1A[2K[1A[2K[1A[2K[0Gpkgs/main/noarch                                   852.8kB @   2.8MB/s  0.3s
    [+] 0.4s
    pkgs/main/linux-64 [90m━━━━━━━━━╸[0m[33m━━━━━━━━━━━━━━━[0m   1.0MB /  ??.?MB @   2.9MB/s  0.4s
    pkgs/r/linux-64    [90m━━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━[0m   1.2MB /  ??.?MB @   3.2MB/s  0.4s
    pkgs/r/noarch      [90m━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━[0m   1.1MB /  ??.?MB @   2.9MB/s  0.4s[2K[1A[2K[1A[2K[1A[2K[0G[+] 0.5s
    pkgs/main/linux-64 [90m━━━━━━━━━╸[0m[33m━━━━━━━━━━━━━━[0m   1.6MB @   3.5MB/s             0.5s
    pkgs/r/linux-64    ━━━━━━━━━━━━━━━━━━━━━━━━   1.4MB @   3.1MB/s Finalizing  0.5s
    pkgs/r/noarch      [90m━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━[0m   1.3MB @   2.8MB/s             0.5s[2K[1A[2K[1A[2K[1A[2K[0Gpkgs/r/linux-64                                    @   3.1MB/s  0.5s
    pkgs/r/noarch                                      @   2.8MB/s  0.6s
    [+] 0.6s
    pkgs/main/linux-64 [90m━━━━━━━━━━╸[0m[33m━━━━━━━━━━━━━━[0m   1.6MB /  ??.?MB @   3.5MB/s  0.6s[2K[1A[2K[0G[+] 0.7s
    pkgs/main/linux-64 [90m━━━━━━━━━━━━╸[0m[33m━━━━━━━━━━━━[0m   2.9MB /  ??.?MB @   4.3MB/s  0.7s[2K[1A[2K[0G[+] 0.8s
    pkgs/main/linux-64 [90m━━━━━━━━━━━━━━━╸[0m[33m━━━━━━━━━[0m   3.4MB /  ??.?MB @   4.3MB/s  0.8s[2K[1A[2K[0G[+] 0.9s
    pkgs/main/linux-64 [33m━━━━━━━━━╸[0m[90m━━━━━━━━━━━━━━━[0m   4.0MB /  ??.?MB @   4.5MB/s  0.9s[2K[1A[2K[0G[+] 1.0s
    pkgs/main/linux-64 [33m━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━━━[0m   4.6MB /  ??.?MB @   4.6MB/s  1.0s[2K[1A[2K[0G[+] 1.1s
    pkgs/main/linux-64 [33m━━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━━[0m   4.9MB /  ??.?MB @   4.7MB/s  1.1s[2K[1A[2K[0G[+] 1.2s
    pkgs/main/linux-64 [33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━━━━[0m   5.5MB /  ??.?MB @   4.8MB/s  1.2s[2K[1A[2K[0G[+] 1.3s
    pkgs/main/linux-64 [90m━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━━[0m   6.0MB /  ??.?MB @   4.8MB/s  1.3s[2K[1A[2K[0G[+] 1.4s
    pkgs/main/linux-64 ━━━━━━━━━━━━━━━━━━━━━━━━   6.1MB @   4.8MB/s Finalizing  1.4s[2K[1A[2K[0Gpkgs/main/linux-64                                 @   4.8MB/s  1.4s
    [?25h
    Pinned packages:
      - python 3.7.*
    
    
    Transaction
    
      Prefix: /home/jupyterlab/conda/envs/python
    
      Updating specs:
    
       - bs4==4.10.0
       - ca-certificates
       - certifi
       - openssl
    
    
      Package               Version  Build         Channel                 Size
    ─────────────────────────────────────────────────────────────────────────────
      Install:
    ─────────────────────────────────────────────────────────────────────────────
    
      [32m+ bs4            [0m      4.10.0  hd3eb1b0_0    pkgs/main/noarch        10kB
    
      Upgrade:
    ─────────────────────────────────────────────────────────────────────────────
    
      [31m- ca-certificates[0m    2023.5.7  hbcca054_0    conda-forge                 
      [32m+ ca-certificates[0m  2023.08.22  h06a4308_0    pkgs/main/linux-64     125kB
      [31m- openssl        [0m      1.1.1t  h0b41bf4_0    conda-forge                 
      [32m+ openssl        [0m      1.1.1w  h7f8727e_0    pkgs/main/linux-64       4MB
    
      Downgrade:
    ─────────────────────────────────────────────────────────────────────────────
    
      [31m- beautifulsoup4 [0m      4.11.1  pyha770c72_0  conda-forge                 
      [32m+ beautifulsoup4 [0m      4.10.0  pyh06a4308_0  pkgs/main/noarch        87kB
    
      Summary:
    
      Install: 1 packages
      Upgrade: 2 packages
      Downgrade: 1 packages
    
      Total download: 4MB
    
    ─────────────────────────────────────────────────────────────────────────────
    
    
    [?25l[2K[0G[+] 0.0s
    Downloading      [90m━━━━━━━━━━━━━━━━━━━━━━━[0m   0.0 B                            0.0s
    Extracting       [90m━━━━━━━━━━━━━━━━━━━━━━━[0m       0                            0.0s[2K[1A[2K[1A[2K[0G[+] 0.1s
    Downloading  (4) [33m━━━━━━━━━━━━━━━━━━━━━━━[0m   0.0 B beautifulsoup4             0.0s
    Extracting       [90m━━━━━━━━━━━━━━━━━━━━━━━[0m       0                            0.0s[2K[1A[2K[1A[2K[0Gbs4                                                 10.2kB @  73.2kB/s  0.1s
    beautifulsoup4                                      86.6kB @ 583.2kB/s  0.2s
    ca-certificates                                    125.5kB @ 838.2kB/s  0.2s
    [+] 0.2s
    Downloading  (1) ━━━━━━━━━━╸[33m━━━━━━━━━━━━[0m   2.2MB openssl                    0.1s
    Extracting   (3) [90m━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━━[0m       0 beautifulsoup4             0.0s[2K[1A[2K[1A[2K[0Gopenssl                                              3.9MB @  18.2MB/s  0.2s
    [+] 0.3s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━━[0m       0 beautifulsoup4             0.1s[2K[1A[2K[1A[2K[0G[+] 0.4s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━━[0m       0 beautifulsoup4             0.2s[2K[1A[2K[1A[2K[0G[+] 0.5s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━╸[0m[33m━━━━━━━━━━━━━━━╸[0m[90m━━[0m       0 beautifulsoup4             0.3s[2K[1A[2K[1A[2K[0G[+] 0.6s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━╸[0m[33m━━━━━━━━━━━━━━━━[0m       0 bs4                        0.4s[2K[1A[2K[1A[2K[0G[+] 0.7s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━╸[0m[33m━━━━━━━━━━━━━━━[0m       0 bs4                        0.5s[2K[1A[2K[1A[2K[0G[+] 0.8s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━━╸[0m[33m━━━━━━━━━━━━━━[0m       0 bs4                        0.6s[2K[1A[2K[1A[2K[0G[+] 0.9s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━━━╸[0m[33m━━━━━━━━━━━━━[0m       0 bs4                        0.7s[2K[1A[2K[1A[2K[0G[+] 1.0s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━━━━╸[0m[33m━━━━━━━━━━━━[0m       0 ca-certificates            0.8s[2K[1A[2K[1A[2K[0G[+] 1.1s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━━━━━╸[0m[33m━━━━━━━━━━━[0m       0 ca-certificates            0.9s[2K[1A[2K[1A[2K[0G[+] 1.2s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [90m━━━━━━━━━━━━╸[0m[33m━━━━━━━━━━[0m       0 ca-certificates            1.0s[2K[1A[2K[1A[2K[0G[+] 1.3s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━╸[0m[90m━━━━━━━━━━━━━━━[0m       0 ca-certificates            1.1s[2K[1A[2K[1A[2K[0G[+] 1.4s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━╸[0m[90m━━━━━━━━━━━━━━[0m       0 openssl                    1.2s[2K[1A[2K[1A[2K[0G[+] 1.5s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━━╸[0m[90m━━━━━━━━━━━━━[0m       0 openssl                    1.3s[2K[1A[2K[1A[2K[0G[+] 1.6s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━━━━╸[0m[90m━━━━━━━━━━━[0m       0 openssl                    1.4s[2K[1A[2K[1A[2K[0G[+] 1.7s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━━━━━╸[0m[90m━━━━━━━━━━[0m       0 openssl                    1.5s[2K[1A[2K[1A[2K[0G[+] 1.8s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━━━━━━╸[0m[90m━━━━━━━━━[0m       0 beautifulsoup4             1.6s[2K[1A[2K[1A[2K[0G[+] 1.9s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (4) [33m━━━━━━━━━━━━━━╸[0m[90m━━━━━━━━[0m       0 beautifulsoup4             1.7s[2K[1A[2K[1A[2K[0G[+] 2.0s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (3) ━━━━╸[33m━━━━━━━━━━━━━━━━━━[0m       1 bs4                        1.8s[2K[1A[2K[1A[2K[0G[+] 2.1s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting   (2) ━━━━━━━━━━╸[33m━━━━━━━━━━━━[0m       2 ca-certificates            1.9s[2K[1A[2K[1A[2K[0G[+] 2.2s
    Downloading      ━━━━━━━━━━━━━━━━━━━━━━━   4.1MB                            0.2s
    Extracting       ━━━━━━━━━━━━━━━━━━━━━━━       4                            2.0s[2K[1A[2K[1A[2K[0G[?25h
    Downloading and Extracting Packages
    
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    Collecting nbformat==4.2.0
      Downloading nbformat-4.2.0-py2.py3-none-any.whl (153 kB)
    [2K     [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m153.3/153.3 kB[0m [31m19.0 MB/s[0m eta [36m0:00:00[0m
    [?25hRequirement already satisfied: ipython-genutils in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from nbformat==4.2.0) (0.2.0)
    Requirement already satisfied: jsonschema!=2.5.0,>=2.4 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from nbformat==4.2.0) (4.17.3)
    Requirement already satisfied: jupyter-core in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from nbformat==4.2.0) (4.12.0)
    Requirement already satisfied: traitlets>=4.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from nbformat==4.2.0) (5.9.0)
    Requirement already satisfied: attrs>=17.4.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (23.1.0)
    Requirement already satisfied: importlib-metadata in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (4.11.4)
    Requirement already satisfied: importlib-resources>=1.4.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (5.12.0)
    Requirement already satisfied: pkgutil-resolve-name>=1.3.10 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (1.3.10)
    Requirement already satisfied: pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (0.19.3)
    Requirement already satisfied: typing-extensions in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (4.5.0)
    Requirement already satisfied: zipp>=3.1.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from importlib-resources>=1.4.0->jsonschema!=2.5.0,>=2.4->nbformat==4.2.0) (3.15.0)
    Installing collected packages: nbformat
      Attempting uninstall: nbformat
        Found existing installation: nbformat 5.8.0
        Uninstalling nbformat-5.8.0:
          Successfully uninstalled nbformat-5.8.0
    [31mERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
    jupyter-server 1.24.0 requires nbformat>=5.2.0, but you have nbformat 4.2.0 which is incompatible.
    nbclient 0.7.4 requires nbformat>=5.1, but you have nbformat 4.2.0 which is incompatible.
    nbconvert 7.4.0 requires nbformat>=5.1, but you have nbformat 4.2.0 which is incompatible.[0m[31m
    [0mSuccessfully installed nbformat-4.2.0



```python
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

## Define Graphing Function


In this section, we define the function `make_graph`. You don't have to know how the function works, you should only care about the inputs. It takes a dataframe with stock data (dataframe must contain Date and Close columns), a dataframe with revenue data (dataframe must contain Date and Revenue columns), and the name of the stock.



```python
def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"), vertical_spacing = .3)
    stock_data_specific = stock_data[stock_data.Date <= '2021--06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), y=stock_data_specific.Close.astype("float"), name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), y=revenue_data_specific.Revenue.astype("float"), name="Revenue"), row=2, col=1)
    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
    fig.update_layout(showlegend=False,
    height=900,
    title=stock,
    xaxis_rangeslider_visible=True)
    fig.show()
```

## Question 1: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is `TSLA`.



```python
tesla = yf.Ticker('TSLA')

```

Using the ticker object and the function `history` extract stock information and save it in a dataframe named `tesla_data`. Set the `period` parameter to `max` so we get information for the maximum amount of time.



```python
tesla_data = tesla.history(period = 'max')
tesla_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-06-29</th>
      <td>1.266667</td>
      <td>1.666667</td>
      <td>1.169333</td>
      <td>1.592667</td>
      <td>281494500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2010-06-30</th>
      <td>1.719333</td>
      <td>2.028000</td>
      <td>1.553333</td>
      <td>1.588667</td>
      <td>257806500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2010-07-01</th>
      <td>1.666667</td>
      <td>1.728000</td>
      <td>1.351333</td>
      <td>1.464000</td>
      <td>123282000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2010-07-02</th>
      <td>1.533333</td>
      <td>1.540000</td>
      <td>1.247333</td>
      <td>1.280000</td>
      <td>77097000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2010-07-06</th>
      <td>1.333333</td>
      <td>1.333333</td>
      <td>1.055333</td>
      <td>1.074000</td>
      <td>103003500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-09-18</th>
      <td>271.160004</td>
      <td>271.440002</td>
      <td>263.760010</td>
      <td>265.279999</td>
      <td>101543300</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-19</th>
      <td>264.350006</td>
      <td>267.850006</td>
      <td>261.200012</td>
      <td>266.500000</td>
      <td>103704000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-20</th>
      <td>267.040009</td>
      <td>273.929993</td>
      <td>262.459991</td>
      <td>262.589996</td>
      <td>122514600</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-21</th>
      <td>257.850006</td>
      <td>260.859985</td>
      <td>254.210007</td>
      <td>255.699997</td>
      <td>119531000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-22</th>
      <td>257.399994</td>
      <td>257.790009</td>
      <td>244.479996</td>
      <td>244.880005</td>
      <td>127024300</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>3332 rows × 7 columns</p>
</div>



**Reset the index** using the `reset_index(inplace=True)` function on the tesla_data DataFrame and display the first five rows of the `tesla_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 1 to the results below.



```python
tesla_data.reset_index(inplace=True)
tesla_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-29</td>
      <td>1.266667</td>
      <td>1.666667</td>
      <td>1.169333</td>
      <td>1.592667</td>
      <td>281494500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-30</td>
      <td>1.719333</td>
      <td>2.028000</td>
      <td>1.553333</td>
      <td>1.588667</td>
      <td>257806500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-07-01</td>
      <td>1.666667</td>
      <td>1.728000</td>
      <td>1.351333</td>
      <td>1.464000</td>
      <td>123282000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-07-02</td>
      <td>1.533333</td>
      <td>1.540000</td>
      <td>1.247333</td>
      <td>1.280000</td>
      <td>77097000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-07-06</td>
      <td>1.333333</td>
      <td>1.333333</td>
      <td>1.055333</td>
      <td>1.074000</td>
      <td>103003500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Question 2: Use Webscraping to Extract Tesla Revenue Data


Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm Save the text of the response as a variable named `html_data`.



```python
url = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm'
html_data = requests.get(url).text

```

Parse the html data using `beautiful_soup`.



```python
soup = BeautifulSoup(html_data)
soup
```




    <!DOCTYPE html>
    <!--[if lt IE 7]>      <html class="no-js lt-ie9 lt-ie8 lt-ie7"> <![endif]--><!--[if IE 7]>         <html class="no-js lt-ie9 lt-ie8"> <![endif]--><!--[if IE 8]>         <html class="no-js lt-ie9"> <![endif]--><!--[if gt IE 8]><!--><html class="no-js"> <!--<![endif]-->
    <head>
    <meta charset="utf-8"/>
    <meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible"/>
    <link href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue" rel="canonical"/>
    <title>Tesla Revenue 2010-2022 | TSLA | MacroTrends</title>
    <meta content="Tesla annual/quarterly revenue history and growth rate from 2010 to 2022. Revenue can be defined as the amount of money a company receives from its customers in exchange for the sales of goods or services.  Revenue is the top line item on an income statement from which all costs and expenses are subtracted to arrive at net income.    
    				
    				&lt;ul style='margin-top:10px;'&gt;
    				&lt;li&gt;Tesla revenue for the quarter ending September 30, 2022 was &lt;strong&gt;$21.454B&lt;/strong&gt;, a &lt;strong&gt;55.95% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla revenue for the twelve months ending September 30, 2022 was &lt;strong&gt;$74.863B&lt;/strong&gt;, a &lt;strong&gt;59.8% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2021 was &lt;strong&gt;$53.823B&lt;/strong&gt;, a &lt;strong&gt;70.67% increase&lt;/strong&gt; from 2020.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2020 was &lt;strong&gt;$31.536B&lt;/strong&gt;, a &lt;strong&gt;28.31% increase&lt;/strong&gt; from 2019.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2019 was &lt;strong&gt;$24.578B&lt;/strong&gt;, a &lt;strong&gt;14.52% increase&lt;/strong&gt; from 2018.&lt;/li&gt;
    				&lt;/ul&gt;" name="description"/>
    <meta content="" name="robots"/>
    <link href="/assets/images/icons/FAVICON/macro-trends_favicon.ico" rel="shortcut icon" type="image/x-icon"/>
    <meta content="1228954C688F5907894001CD8E5E624B" name="msvalidate.01"/>
    <meta content="6MnD_3iDtAP1ZyoGK1YMyVIVck4r5Ws80I9xD3ue4_A" name="google-site-verification"/>
    <!-- Load in Roboto Font -->
    <link href="https://fonts.googleapis.com/css?family=Roboto:400,600,700" rel="stylesheet"/>
    <!-- Bootstrap -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet"/> <!--for Bootstrap CDN version-->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" rel="stylesheet"/>
    <!-- Font Awesome -->
    <link href="//stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet"/> <!--for Font Awesome CDN version-->
    <!-- Jquery, Bootstrap and Menu Javascript -->
    <script crossorigin="anonymous" integrity="sha256-ZosEbRLbNQzLpnKIkEdrPv7lOy9C27hHQ+Xp8a4MxAQ=" src="//code.jquery.com/jquery-1.12.4.min.js"></script>
    <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
    <!-- Modernizr for cross-browser support -->
    <script src="/assets/javascript/modernizr-2.6.2-respond-1.1.0.min.js" type="text/javascript"></script>
    <!-- Latest compiled and minified CSS -->
    <link href="//www.fuelcdn.com/fuelux/3.13.0/css/fuelux.min.css" rel="stylesheet"/>
    <!-- Latest compiled and minified JavaScript -->
    <script src="//www.fuelcdn.com/fuelux/3.13.0/js/fuelux.min.js"></script>
    <!-- Twitter Card data -->
    <meta content="summary_large_image" name="twitter:card"/>
    <meta content="@tmacrotrends" name="twitter:site"/>
    <meta content="Tesla Revenue 2010-2022 | TSLA" name="twitter:title"/>
    <meta content="Tesla annual/quarterly revenue history and growth rate from 2010 to 2022. Revenue can be defined as the amount of money a company receives from its customers in exchange for the sales of goods or services.  Revenue is the top line item on an income statement from which all costs and expenses are subtracted to arrive at net income.    
    				
    				&lt;ul style='margin-top:10px;'&gt;
    				&lt;li&gt;Tesla revenue for the quarter ending September 30, 2022 was &lt;strong&gt;$21.454B&lt;/strong&gt;, a &lt;strong&gt;55.95% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla revenue for the twelve months ending September 30, 2022 was &lt;strong&gt;$74.863B&lt;/strong&gt;, a &lt;strong&gt;59.8% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2021 was &lt;strong&gt;$53.823B&lt;/strong&gt;, a &lt;strong&gt;70.67% increase&lt;/strong&gt; from 2020.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2020 was &lt;strong&gt;$31.536B&lt;/strong&gt;, a &lt;strong&gt;28.31% increase&lt;/strong&gt; from 2019.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2019 was &lt;strong&gt;$24.578B&lt;/strong&gt;, a &lt;strong&gt;14.52% increase&lt;/strong&gt; from 2018.&lt;/li&gt;
    				&lt;/ul&gt;" name="twitter:description"/>
    <!-- Open Graph data -->
    <meta content="https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue" property="og:url"/>
    <meta content="Tesla Revenue 2010-2022 | TSLA" property="og:title"/>
    <meta content="Tesla annual/quarterly revenue history and growth rate from 2010 to 2022. Revenue can be defined as the amount of money a company receives from its customers in exchange for the sales of goods or services.  Revenue is the top line item on an income statement from which all costs and expenses are subtracted to arrive at net income.    
    				
    				&lt;ul style='margin-top:10px;'&gt;
    				&lt;li&gt;Tesla revenue for the quarter ending September 30, 2022 was &lt;strong&gt;$21.454B&lt;/strong&gt;, a &lt;strong&gt;55.95% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla revenue for the twelve months ending September 30, 2022 was &lt;strong&gt;$74.863B&lt;/strong&gt;, a &lt;strong&gt;59.8% increase&lt;/strong&gt; year-over-year.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2021 was &lt;strong&gt;$53.823B&lt;/strong&gt;, a &lt;strong&gt;70.67% increase&lt;/strong&gt; from 2020.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2020 was &lt;strong&gt;$31.536B&lt;/strong&gt;, a &lt;strong&gt;28.31% increase&lt;/strong&gt; from 2019.&lt;/li&gt;
    				&lt;li&gt;Tesla annual revenue for 2019 was &lt;strong&gt;$24.578B&lt;/strong&gt;, a &lt;strong&gt;14.52% increase&lt;/strong&gt; from 2018.&lt;/li&gt;
    				&lt;/ul&gt;" property="og:description"/>
    <!-- JQXGRID STYLES AND JAVASCRIPT -->
    <link href="/assets/php/jqfiles/jqwidgets/styles/jqx.base.css" rel="stylesheet" type="text/css"/>
    <link href="/assets/php/jqfiles/jqwidgets/styles/jqx.bootstrap.css" rel="stylesheet" type="text/css"/>
    <!-- LOAD THESE SCRIPTS EARLY SO THE TICKER INPUT FIELD IS STYLED INSTANTLY -->
    <script src="/assets/php/jqfiles/jqwidgets/jqxcore.js" type="text/javascript"></script>
    <script src="/assets/php/jqfiles/jqwidgets/jqxdata.js" type="text/javascript"></script>
    <script src="/assets/php/jqfiles/jqwidgets/jqxinput.js" type="text/javascript"></script>
    <!-- Styling for search box -->
    <link href="/assets/php/jquery-typeahead/jquery.typeahead_pages.css" rel="stylesheet" type="text/css"/>
    <!-- Search box javascript -->
    <script src="/assets/php/jquery-typeahead/jquery.typeahead.min.js"></script>
    <link href="//cdnjs.cloudflare.com/ajax/libs/select2/4.0.3/css/select2.min.css" rel="stylesheet"/>
    <script src="//cdnjs.cloudflare.com/ajax/libs/select2/4.0.3/js/select2.min.js"></script>
    <!-- ToolTips -->
    <script src="/assets/php/tipped-4.6.1/js/tipped/tipped.js"></script>
    <link href="/assets/php/tipped-4.6.1/css/tipped/tipped.css" rel="stylesheet"/>
    <!-- START IC AD INSERT -->
    <script>InvestingChannelQueue = window.InvestingChannelQueue || [];</script>
    <script async="" src="https://u5.investingchannel.com/static/uat.js"></script>
    <script type="text/javascript">
        
            //Push Run command with the API-Key, so that UAT will start processing publishers request.
            InvestingChannelQueue.push(function() {
                ic_page = InvestingChannel.UAT.Run("df17ac1e-cc7f-11e8-82a5-0abbb61c4a6a");        
            });
    		
    		var tickerValue = 'TSLA';			
            var oopDivTag;
    		var subLeaderboardTag;
    		var rightSidebarTag1;
    		var rightSidebarTag2;
    		var searchButtonTag;
    		var partner_center_tag;
    		var videoTag;
    		var ic_3x7_1;
     		//var IC_D_300x250_BCC;
    		//var IC_D_3x7_BCC;
       
            //To define new tags/out of page tags.
            InvestingChannelQueue.push(function() {
    			
    			ic_page.setKval({'t': tickerValue});
    			
                //videoTag = ic_page.defineNativeTag("Macrotrends/fundamentalanalysis","3x6, 728x90, Fluid","IC_D_3x6",35);
    			
                oopDivTag = ic_page.defineOutOfPageTag("Macrotrends/fundamentalanalysis","oopDivTag_1");
    			oopDivTag.setKval({"adslot":"IC_OOP_1"});
                
    			
    			LeaderboardTag = ic_page.defineTag("Macrotrends/fundamentalanalysis","970x250,728x90,970x90,fluid", "IC_D_970x250_1");
    			LeaderboardTag.setKval({"adslot":"IC_D_970x250_1"});
    
    
    			subLeaderboardTag = ic_page.defineTag("Macrotrends/fundamentalanalysis","728x90","ic_728x90_1");
    			subLeaderboardTag.setKval({"adslot":"IC_728x90_1"});
    			
    			
    			rightSidebarTag1 = ic_page.defineTag("Macrotrends/fundamentalanalysis","300x250,Fluid","ic_300x250_1");
    			rightSidebarTag1.setKval({"adslot":"IC_300x250_1"});
    			
    			
    			rightSidebarTag2 = ic_page.defineTag("Macrotrends/fundamentalanalysis","300x600,300x250,160x600,300x1050,Fluid","ic_300x600_1");
    			rightSidebarTag2.setKval({"adslot":"IC_300x600_1"});
    			
    			
    			searchButtonTag = ic_page.defineTag("Macrotrends/fundamentalanalysis","88x31","ic_88x31_1");
    			searchButtonTag.setKval({"pc":"pc","adslot":"IC_88x31"});
    			
    			partner_center_tag = ic_page.defineTag("macrotrends/fundamentalanalysis","728x214, 728x90","IC_728x214_1");
    			partner_center_tag.setKval({"pc":"pc","adslot":"d_728x90_2"});
    
    			ic_3x7_1 = ic_page.defineNativeTag("macrotrends/fundamentalanalysis","3x7,728x90,Fluid","IC_3x7_1", 35);
    			
    			//IC_D_300x250_BCC = ic_page.defineTag(adCategory,"300x250,Fluid","IC_D_300x250_BCC");
    			//IC_D_300x250_BCC.setKval({"adslot":"IC_D_300x250_BCC"});
    
    			//IC_D_3x7_BCC = ic_page.defineTag(adCategory,"3x7, Fluid","IC_D_3x7_BCC");
    			//IC_D_3x7_BCC.setKval({"adslot":"IC_D_3x7_BCC"});
    			
    
            });
        
            //To render tags.
    			InvestingChannelQueue.push(function() {
                ic_page.renderTags();
            });
            
        </script>
    <!-- END IC AD INSERT -->
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script async="" src="https://www.googletagmanager.com/gtag/js?id=UA-62099500-1"></script>
    <script>
    		  window.dataLayer = window.dataLayer || [];
    		  function gtag(){dataLayer.push(arguments);}
    		  gtag('js', new Date());
    
    		  gtag('config', 'UA-62099500-1');
    		</script>
    <!-- Google tag (gtag.js) -->
    <script async="" src="https://www.googletagmanager.com/gtag/js?id=G-3KL0LYERBH"></script>
    <script>
    		  window.dataLayer = window.dataLayer || [];
    		  function gtag(){dataLayer.push(arguments);}
    		  gtag('js', new Date());
    
    		  gtag('config', 'G-3KL0LYERBH');
    		</script>
    <!--<script>
    			(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    			(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    			m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    			})(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    
    			ga('create', 'UA-62099500-1', 'auto');
    			ga('send', 'pageview');
    			
    			
    			
    		   
    			//Send one event to GA at 30 seconds to control bounce rate
    			setTimeout("ga('send','event','Engaged User','30 Second Engagement')",30000); 
    
    
    		  //This code sends events to ga every 30 seconds when the window is in focus
    			var count = 0;
    			var myInterval;
    					
    			// Active
    			window.addEventListener('load', startTimer);
    			window.addEventListener('focus', startTimer);
    
    			// Inactive
    			window.addEventListener('blur', stopTimer);
    
    			function timerHandler() {
    				count++;
    				
    				if(count % 60 == 0 && count <= 1800) {
    					
    					var interval = (count/60);
    					interval = interval.toFixed(0);
    					
    					var action = interval + " Minute Engagement";
    					
    					ga('send','event','Engaged User',action);
    
    					
    				}
    			
    			}
    
    			// Start timer
    			function startTimer() {
    			myInterval = window.setInterval(timerHandler, 1000);
    			}
    
    			// Stop timer
    			function stopTimer() {
    			window.clearInterval(myInterval);
    			}
    			
    			
    
    		</script>-->
    <style> 
    
    #style-1::-webkit-scrollbar-track
    {
    	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3);
    	border-radius: 3px;
    	background-color: #F5F5F5;
    }
    
    #style-1::-webkit-scrollbar
    {
    	width: 18px;
    	background-color: #F5F5F5;
    }
    
    #style-1::-webkit-scrollbar-thumb
    {
    	border-radius: 3px;
    	-webkit-box-shadow: inset 0 0 6px rgba(0,0,0,.3);
    	background-color: #5B9BD5;
    }
    
    html {
    	width:100%;
    	position: relative;
    	min-height: 100%;
    }
    
    body {
    	
    	width:100%;
    
    	/* Margin bottom by footer height */
    	  margin-bottom: 80px;
    	  color: #444;
    	  background-color:#fff;
    	  font-family: 'Roboto', sans-serif;
    	  font-size:14px;
    }
    
    
    
    
    
    .header_content_container {
    	
    	min-width: 1280px;
    	padding: 0px;
    }
    
    .main_content_container {
    	
    	min-width: 1280px;
    	max-width: 1280px;
    	padding: 0px 30px 100px 30px;
    	
    }
    
    .sub_main_content_container {
    	
    	
    }
    
    
    
    #main_content {
    	
    	padding:0px 20px 0px 0px;
    	width:826px;
        float:left;
    	
    }
    
    #right_sidebar {
    	
      width: 300px;
      float:left;
      height:3200px;
    	
    }
    
    #sticky_ad_left {
    	
      position: -webkit-sticky;
      position: sticky;
      top: 30px;
    	
    	
    }
    
    #sticky_ad_right {
    	
      position: -webkit-sticky;
      position: sticky;
      top: 30px;
    	
    	
    }
    
    
    
    
    
    .footer {
      position: absolute;
      bottom: 0;
      width: 100%;
      /* Set the fixed height of the footer here */
      height: 100px;
      margin-top: 10px;	
      padding: 30px 20px 20px 20px;
      color:#fff !important;
      background-color:#444;
      text-align: center;
      font-size:16px;
    }
    
    .footer a {
      color:#fff !important;
    }
    
    .ticker_search_box {
    	
    	background-color:#F5F5F5;
    	border: 1px solid #E0E0E0;
    	border-bottom:none;
    	padding:10px 30px 10px 10px;
    	margin:0px 0px 0px 0px;
    	text-align:center;
    	
    }
    
    .related_tickers {
    	
    	width:100%;
    	background-color:#F5F5F5;
    	border: 1px solid #E0E0E0;
    	border-top: 0px;
    	padding:3px 30px 3px 10px;
    	margin:0px 0px 0px 0px;
    	text-align:center;
    	
    }
    
    .statement_type_select {
    
    	width:100%;
    	height:28px;
    	
    }
    
    .frequency_select {
    
    	width:100%;
    	height:28px;
    	font-weight:600;
    	
    }
    
    
    .select2 {
    	
    	text-align:left;
    	font-weight:600;
    	
    	}
    	
    #jqxInput {
    
    		width:100%;
    		height:28px;
    		
    }
    
    
    
    .header__parent_container {
    
    	width:100%;
    	height:50px;
    	padding:15px 0px 10px -20px; 
    	margin:0px 0px 0px 0px;
    	background-color:#444;
    
    }
    
    .header_container {
    
    	width:100%;
    	height:50px;
    	padding:15px 0px 10px -20px; 
    	margin:0px 0px 0px 0px;
    	background-color:#444;
    
    }
    
    .header_logo {
    	
    	padding-top:10px;
    	margin-left:50px;
    	
    }
    
    .menu_parent_container {
    	
    	width:100%;
    	height:34px;
    	font-size:16px;
    	padding:15px 0px 10px -20px; 
    	margin:0px 0px 0px 0px;
    	background-color:#0089de;
    }
    
    .menu_container {
    	
    	width:1280px;
    	height:34px;
    	font-size:16px;
    	padding:11px 0px 0px -20px; 
    	margin: 0 auto;
    	background-color:#0089de;
    	z-index:1000;
    }
    
    .menu_item {
    
    	height:34px;
    	float:left;
    	font-size:14px;
    	font-weight:bold;
    	color:#fff;
    	text-align:center;
    	padding:7px 16px 0px 16px;	
    
    }
    
    .menu_item:hover
    {
    	background-color:#32a0e4;
    	cursor: pointer;
    }
    
    .menu_item a
    {
    	color:#fff;
    	cursor: pointer;
    }
    
    .menu_item a:hover
    {
    	text-decoration:none;
    	cursor: pointer;
    }
    
    .leaderboard_ad {
    
    	margin-top:20px;
    	margin-bottom:20px;
    	text-align:center;
    	min-height:100px;
    
    }
    
    #filter_result_count {
    	
    	width:100%;
    	text-align:center;
    	font-size:24px;
    	font-weight:bold;
    	padding:10px 15px;
    	background-color:#efefef;
    	border: 1px solid #dfdfdf;
    	margin:20px;
    	
    }
    
    
    select {
      color: #444;
      background-color: #FFF;
      border: 1px solid #AAA;
      border-radius: 4px;
      box-sizing: border-box;
      cursor: pointer;
      display: block;
      height:40px;
      line-height: 40px;
    }
    
    .historical_data_table  {
        table-layout: fixed;
    	margin:20px;
    }
    
    .historical_data_table tbody tr td {
    	
    	padding:6px;
    	vertical-align: middle !important;
    
    }
    
    
    .descriptors {
    	
    	text-align:center;
    	font-size:14px;
    	padding:15px;
    	
    }
    
    .td_metric_name {
    	
    	width:110px;
    	padding-top:17px;
    	
    }
    
    .metric_link {
    	
    	font-size:14px;
    	font-weight:bold;
    
    }
    
    .help_icon {
    	
    	width:15px;
    	height:18px; 
    	padding-bottom:3px;
    	
    }
    
    .td_min_value {
    	
    	width:75px;
    	text-align:center;
    	font-size:13px;
    	
    }
    
    .td_max_value {
    	
    	width:75px;
    	text-align:center;
    	font-size:13px;
    	
    }
    
    #myCombobox .form-control {
    	
    	background-color: #99d5ff;
    
    	
    }
    
    .dropdown-toggle {
    	
    	height:24px;
    	padding-top:0px;
    	padding-left:7px;
    	width:24px;
    	
    }
    
    .dropdown-menu-right {
    	
    	min-width:75px;
    	font-size:13px;
    	
    }
    
    .form-control {
    	
    	font-size:12px;	
    	padding:5px 10px;
    	height:24px;
    
    	
    }
    
    #myPills1 {
    	
    	margin:0px 15px 10px 0px;
    	
    }
    
    #jqxgrid {
    	
    	border-radius:0px;
    	
    }
    
    .jqx-widget-header {
    	
        font-family: 'Roboto', sans-serif;
    	font-size:13px;	
    	
    }
    
    .jqx-item {
    	
        font-family: 'Roboto', sans-serif;
    	font-size: 13px;
    	
    }
    
    .jqx-widget-content {
    	
    	border-color: #E0E0E0;
    	
    }
    
    #jqxgrid .jqx-grid-cell {
    	
    	border-color: #E0E0E0;
    	
    }
    
    #jqxgrid .jqx-grid-cell-pinned {
    	
    	border-color: #E0E0E0;
    	background-color: #F5F5F5;
    	
    }
    
    #jqxgrid .jqx-grid-column-header {
    	
    	border-color: #E0E0E0;
    	background-color: #F5F5F5;
    	
    }
    
    .clear_zero {
    
    	height:0px;
    
    }
    
    
    
    /* Styles for Popup Charts */
    
    .tpd-size-large {
    	
    	margin:0px;	
    	padding: 0px;
    }
    
    .popup_window_wrapper {
    	
    	margin:15px;
    	
    }
    
    .popup_stock_name {
    
    	font-size:16px;
    	font-weight:bold;
    	margin:5px;
    
    }
    
    .popup_stock_attributes {
    
    	font-size:13px;
    	font-weight:bold;
    	margin:5px;
    
    }
    
    .popup_stock_description {
    
    	font-size:12px;
    	margin:5px;
    
    }
    
    .jqx-input {
    	
    	font-size:14px;
    	
    } 
    
    .jqx-menu-item {
    	
    	font-size:14px;
    	
    }
    
    .jqx-input {
    	
    	padding:5px 10px;
    	
    }
    
    .nav-tabs {
        border: 1px solid #E0E0E0;
    	background-color:#F5F5F5;
    	padding: 3px 5px 0px 5px;
    	margin: 0px 0px 10px 0px;
    }
    
    .nav-tabs>li>a {
    	font-size:13px;
    	padding:7px 11px;
    	font-weight:600;
        margin-right: 0px;
        line-height: 1.42857143;
        border: 0px;
        border-radius: 0px 0px 0 0;
    	background-color:#F5F5F5;
    
    }
    
    .nav-tabs>li>a .active {
        margin-right: 0px;
        line-height: 1.42857143;
        border: 1px solid #E0E0E0;
        border-radius: 0px 0px 0 0;
    	background-color:#F5F5F5;
    
    }
    
    .nav-tabs>li>a:hover { 
        background-color: #F5F5F5;
    	text-decoration: underline;
    
    }
    
    .donate_buttons {
    
    	margin-left:20px;
    	
    	}
    
    .modal-body {
    
    	margin:10px 40px 20px 40px;
    	text-align:left;
    	font-size:18px;
    
    }
    
    .modal-body li {
    
    	margin-top:20px;
    	font-size:14px;
    
    }
    
    
    .modal_title {
    
    
    	text-align:center;
    	margin-bottom:30px;
    
    }
    
    .modal-body th{
    
    	margin-left:10px;
    	font-size:14px;
    }
    
    .modal-body td {
    
    	color: #337ab7;
    	margin-left:10px;
    	font-size:14px;
    }
    
    .modal_button {
    
    	margin-top:50px;
    	text-align:center;
    	font-size:16px;
    
    }	
    
    
    </style>
    </head>
    <body class="fuelux">
    <!--[if lt IE 7]>
                <p class="browsehappy">You are using an <strong>outdated</strong> browser. Please <a href="https://browsehappy.com/">upgrade your browser</a> to improve your experience.</p>
            <![endif]-->
    <div class="header_content_container container-fluid">
    <div class="header_parent_container">
    <div class="header_container">
    <div class="header_logo col-xs-2">
    <a class="logo" href="https://www.macrotrends.net" title="MacroTrends Home Page"><img src="/assets/images/logo_bright1.png"/></a>
    </div>
    <div class="col-xs-1 pull-right" style="padding-top:8px; margin-right:10px; margin-left:0px; padding-left:0px;">
    <div id="ic_88x31_1">
    </div>
    </div>
    <div class="col-xs-5 pull-right" style="padding-top:8px;">
    <form>
    <div class="typeahead__container">
    <div class="typeahead__field">
    <span class="typeahead__query">
    <input autocomplete="off" autofocus="" class="js-typeahead" name="q" placeholder="Search over 200,000 charts..." type="search"/>
    </span>
    <span class="typeahead__button">
    <button type="submit">
    <span class="typeahead__search-icon"></span>
    </button>
    </span>
    </div>
    </div>
    </form>
    </div>
    </div>
    </div>
    <div class="menu_parent_container">
    <div class="menu_container">
    <a href="/stocks/stock-screener"><div class="menu_item">Stock Screener</div></a>
    <a href="/stocks/research"><div class="menu_item">Stock Research</div></a>
    <a href="/charts/stock-indexes"><div class="menu_item">Market Indexes</div></a>
    <a href="/charts/precious-metals"><div class="menu_item">Precious Metals</div></a>
    <a href="/charts/energy"><div class="menu_item">Energy</div></a>
    <a href="/charts/commodities"><div class="menu_item">Commodities</div></a>
    <a href="/charts/exchange-rates"><div class="menu_item">Exchange Rates</div></a>
    <a href="/charts/interest-rates"><div class="menu_item">Interest Rates</div></a>
    <a href="/charts/economy"><div class="menu_item">Economy</div></a>
    <a href="/countries/topic-overview"><div class="menu_item">Global Metrics</div></a>
    </div>
    </div>
    </div>
    <div class="main_content_container container-fluid" id="main_content_container">
    <div class="adx_top_ad col-xs-12" id="ic_leaderboard" style="margin: 20px 20px 30px 20px; min-height:265px; text-align:center;">
    <div id="IC_D_970x250_1"></div>
    <!--Smartad # 4058: Macrotrends - 970x250 Image - Placement 2-->
    <!--<iframe id="dianomi_leaderboard" WIDTH="970" HEIGHT="250" SCROLLING="NO" src="//www.dianomi.com/smartads.epl?id=4058"  style="height: 250px; border: none; overflow: hidden;"></iframe>-->
    </div>
    <div style="margin:20px 20px 20px 5px;">
    <h2 style="margin-left:0px; font-weight:600; color:#444;">Tesla Revenue 2010-2022 | TSLA</h2>
    </div>
    <div class="sub_main_content_container">
    <div id="main_content">
    <div class="navigation_tabs" style="margin-bottom:20px;">
    <ul class="nav nav-tabs" id="myTabs" style="font-size:15px;">
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/stock-price-history">Prices</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/financial-statements">Financials</a></li>
    <li class="active"><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue">Revenue &amp; Profit</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/total-assets">Assets &amp; Liabilities</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/profit-margins">Margins</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/pe-ratio">Price Ratios</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/current-ratio">Other Ratios</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/dividend-yield-history">Other Metrics</a></li>
    </ul>
    <ul class="nav nav-tabs" id="myTabs" style="font-size:15px;">
    <li class="active"><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue">Revenue</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/gross-profit">Gross Profit</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/operating-income">Operating Income</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/ebitda">EBITDA</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/net-income">Net Income</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/eps-earnings-per-share-diluted">EPS</a></li>
    <li><a href="https://www.macrotrends.net/stocks/charts/TSLA/tesla/shares-outstanding">Shares Outstanding</a></li>
    </ul>
    </div>
    <div style="background-color:#fff; margin: 0px 0px 20px 0px; padding:20px 30px; border:1px solid #dfdfdf;">
    <span style="color:#444; line-height: 1.8;">Tesla annual/quarterly revenue history and growth rate from 2010 to 2022. Revenue can be defined as the amount of money a company receives from its customers in exchange for the sales of goods or services.  Revenue is the top line item on an income statement from which all costs and expenses are subtracted to arrive at net income.    
    				
    				<ul style="margin-top:10px;">
    <li>Tesla revenue for the quarter ending September 30, 2022 was <strong>$21.454B</strong>, a <strong>55.95% increase</strong> year-over-year.</li>
    <li>Tesla revenue for the twelve months ending September 30, 2022 was <strong>$74.863B</strong>, a <strong>59.8% increase</strong> year-over-year.</li>
    <li>Tesla annual revenue for 2021 was <strong>$53.823B</strong>, a <strong>70.67% increase</strong> from 2020.</li>
    <li>Tesla annual revenue for 2020 was <strong>$31.536B</strong>, a <strong>28.31% increase</strong> from 2019.</li>
    <li>Tesla annual revenue for 2019 was <strong>$24.578B</strong>, a <strong>14.52% increase</strong> from 2018.</li>
    </ul></span>
    </div>
    <div style="background-color:#fff; margin: 30px 0px 30px 0px; text-align:center; min-height:90px;">
    <div id="ic_728x90_1" style="margin:10px 20px;">
    </div>
    </div>
    <div class="ticker_search_box" style="text-align:center;">
    <div style="width:400px; margin-left:20px; border-bottom:none;">
    <script type="text/javascript">
                $(document).ready(function () {
    				                
    					var url = "https://www.macrotrends.net/assets/php/ticker_search_list.php";
    				
                    // prepare the data
                    var source =
                    {
                        datatype: "json",
                        datafields: [
                            { name: 'n' },
    						{ name: 's'}
                        ],
                        url: url
                    };
                    var dataAdapter = new $.jqx.dataAdapter(source);
                    // Create a jqxInput
                    $("#jqxInput").jqxInput({ source: dataAdapter, minLength: 1, placeHolder: "Search for ticker or company name...", items: 20, searchMode: 'containsignorecase', displayMember: "n", valueMember: "s", width: '100%', height: 22, theme: 'bootstrap'});
                    $("#jqxInput").on('select', function (event) {
                        if (event.args) {
                            var item = event.args.item;
    						
    						//Have to split the ticker and slug back out since jqxinput only seems to allow one data value
    						var itemArray = item.value.split("\/"); 
    						var ticker = itemArray[0];
    						var slug = itemArray[1];
                            if (item) {
    							
    														
    								window.location = "https://www.macrotrends.net/stocks/charts/" + ticker + "/" + slug + "/revenue";
    							
    							                        }
                        }
                    });
                });
            </script>
    <input autocomplete="off" id="jqxInput"/>
    </div>
    <div style="width:280px; margin-top: -32px; margin-left:80px; border-bottom:none; float:right;">
    <button class="chart_buttons btn btn-success btn-sm" id="compareStocks" style="margin-right:15px;"><span class="glyphicon glyphicon-stats"></span>  <strong>Compare TSLA With Other Stocks</strong></button>  
    
    </div>
    </div>
    <div style="height:690px; background-color:#fff; border:1px solid #dfdfdf;">
    <iframe frameborder="0" height="680" hspace="0" id="chart_iframe" margin="0px" marginheight="0" marginwidth="0" scrolling="NO" src="https://www.macrotrends.net/assets/php/fundamental_iframe.php?t=TSLA&amp;type=revenue&amp;statement=income-statement&amp;freq=Q" title="Interactive chart: Tesla Revenue 2010-2022 | TSLA" valign="middle" vspace="0" width="800"></iframe>
    </div>
    <div id="ic_video_ad" style="height:317px; margin:30px;">
    <div id="IC_D_3x6"></div>
    </div>
    <div style="background-color:#fff; margin: 30px 0px; padding:10px 30px; border:1px solid #dfdfdf;">
    <iframe frameborder="0" height="300" hspace="0" id="dianomi_below_chart" marginheight="0" marginwidth="0" scrolling="NO" src="//www.dianomi.com/smartads.epl?id=4057" valign="middle" vspace="0" width="100%"></iframe>
    <!--<div id="IC_D_3x7_BCC"></div>-->
    </div>
    <div id="style-1" style="background-color:#fff; height:510px; overflow:auto; margin: 30px 0px 30px 0px; padding:0px 30px 20px 0px; border:1px solid #dfdfdf;">
    <div class="col-xs-6">
    <table class="historical_data_table table">
    <thead>
    <tr>
    <th colspan="2" style="text-align:center">Tesla Annual Revenue<br/><span style="font-size:14px;">(Millions of US $)</span></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:center">2021</td>
    <td style="text-align:center">$53,823</td>
    </tr>
    <tr>
    <td style="text-align:center">2020</td>
    <td style="text-align:center">$31,536</td>
    </tr>
    <tr>
    <td style="text-align:center">2019</td>
    <td style="text-align:center">$24,578</td>
    </tr>
    <tr>
    <td style="text-align:center">2018</td>
    <td style="text-align:center">$21,461</td>
    </tr>
    <tr>
    <td style="text-align:center">2017</td>
    <td style="text-align:center">$11,759</td>
    </tr>
    <tr>
    <td style="text-align:center">2016</td>
    <td style="text-align:center">$7,000</td>
    </tr>
    <tr>
    <td style="text-align:center">2015</td>
    <td style="text-align:center">$4,046</td>
    </tr>
    <tr>
    <td style="text-align:center">2014</td>
    <td style="text-align:center">$3,198</td>
    </tr>
    <tr>
    <td style="text-align:center">2013</td>
    <td style="text-align:center">$2,013</td>
    </tr>
    <tr>
    <td style="text-align:center">2012</td>
    <td style="text-align:center">$413</td>
    </tr>
    <tr>
    <td style="text-align:center">2011</td>
    <td style="text-align:center">$204</td>
    </tr>
    <tr>
    <td style="text-align:center">2010</td>
    <td style="text-align:center">$117</td>
    </tr>
    <tr>
    <td style="text-align:center">2009</td>
    <td style="text-align:center">$112</td>
    </tr>
    </tbody>
    </table>
    </div>
    <div class="col-xs-6">
    <table class="historical_data_table table">
    <thead>
    <tr>
    <th colspan="2" style="text-align:center">Tesla Quarterly Revenue<br/><span style="font-size:14px;">(Millions of US $)</span></th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:center">2022-09-30</td>
    <td style="text-align:center">$21,454</td>
    </tr>
    <tr>
    <td style="text-align:center">2022-06-30</td>
    <td style="text-align:center">$16,934</td>
    </tr>
    <tr>
    <td style="text-align:center">2022-03-31</td>
    <td style="text-align:center">$18,756</td>
    </tr>
    <tr>
    <td style="text-align:center">2021-12-31</td>
    <td style="text-align:center">$17,719</td>
    </tr>
    <tr>
    <td style="text-align:center">2021-09-30</td>
    <td style="text-align:center">$13,757</td>
    </tr>
    <tr>
    <td style="text-align:center">2021-06-30</td>
    <td style="text-align:center">$11,958</td>
    </tr>
    <tr>
    <td style="text-align:center">2021-03-31</td>
    <td style="text-align:center">$10,389</td>
    </tr>
    <tr>
    <td style="text-align:center">2020-12-31</td>
    <td style="text-align:center">$10,744</td>
    </tr>
    <tr>
    <td style="text-align:center">2020-09-30</td>
    <td style="text-align:center">$8,771</td>
    </tr>
    <tr>
    <td style="text-align:center">2020-06-30</td>
    <td style="text-align:center">$6,036</td>
    </tr>
    <tr>
    <td style="text-align:center">2020-03-31</td>
    <td style="text-align:center">$5,985</td>
    </tr>
    <tr>
    <td style="text-align:center">2019-12-31</td>
    <td style="text-align:center">$7,384</td>
    </tr>
    <tr>
    <td style="text-align:center">2019-09-30</td>
    <td style="text-align:center">$6,303</td>
    </tr>
    <tr>
    <td style="text-align:center">2019-06-30</td>
    <td style="text-align:center">$6,350</td>
    </tr>
    <tr>
    <td style="text-align:center">2019-03-31</td>
    <td style="text-align:center">$4,541</td>
    </tr>
    <tr>
    <td style="text-align:center">2018-12-31</td>
    <td style="text-align:center">$7,226</td>
    </tr>
    <tr>
    <td style="text-align:center">2018-09-30</td>
    <td style="text-align:center">$6,824</td>
    </tr>
    <tr>
    <td style="text-align:center">2018-06-30</td>
    <td style="text-align:center">$4,002</td>
    </tr>
    <tr>
    <td style="text-align:center">2018-03-31</td>
    <td style="text-align:center">$3,409</td>
    </tr>
    <tr>
    <td style="text-align:center">2017-12-31</td>
    <td style="text-align:center">$3,288</td>
    </tr>
    <tr>
    <td style="text-align:center">2017-09-30</td>
    <td style="text-align:center">$2,985</td>
    </tr>
    <tr>
    <td style="text-align:center">2017-06-30</td>
    <td style="text-align:center">$2,790</td>
    </tr>
    <tr>
    <td style="text-align:center">2017-03-31</td>
    <td style="text-align:center">$2,696</td>
    </tr>
    <tr>
    <td style="text-align:center">2016-12-31</td>
    <td style="text-align:center">$2,285</td>
    </tr>
    <tr>
    <td style="text-align:center">2016-09-30</td>
    <td style="text-align:center">$2,298</td>
    </tr>
    <tr>
    <td style="text-align:center">2016-06-30</td>
    <td style="text-align:center">$1,270</td>
    </tr>
    <tr>
    <td style="text-align:center">2016-03-31</td>
    <td style="text-align:center">$1,147</td>
    </tr>
    <tr>
    <td style="text-align:center">2015-12-31</td>
    <td style="text-align:center">$1,214</td>
    </tr>
    <tr>
    <td style="text-align:center">2015-09-30</td>
    <td style="text-align:center">$937</td>
    </tr>
    <tr>
    <td style="text-align:center">2015-06-30</td>
    <td style="text-align:center">$955</td>
    </tr>
    <tr>
    <td style="text-align:center">2015-03-31</td>
    <td style="text-align:center">$940</td>
    </tr>
    <tr>
    <td style="text-align:center">2014-12-31</td>
    <td style="text-align:center">$957</td>
    </tr>
    <tr>
    <td style="text-align:center">2014-09-30</td>
    <td style="text-align:center">$852</td>
    </tr>
    <tr>
    <td style="text-align:center">2014-06-30</td>
    <td style="text-align:center">$769</td>
    </tr>
    <tr>
    <td style="text-align:center">2014-03-31</td>
    <td style="text-align:center">$621</td>
    </tr>
    <tr>
    <td style="text-align:center">2013-12-31</td>
    <td style="text-align:center">$615</td>
    </tr>
    <tr>
    <td style="text-align:center">2013-09-30</td>
    <td style="text-align:center">$431</td>
    </tr>
    <tr>
    <td style="text-align:center">2013-06-30</td>
    <td style="text-align:center">$405</td>
    </tr>
    <tr>
    <td style="text-align:center">2013-03-31</td>
    <td style="text-align:center">$562</td>
    </tr>
    <tr>
    <td style="text-align:center">2012-12-31</td>
    <td style="text-align:center">$306</td>
    </tr>
    <tr>
    <td style="text-align:center">2012-09-30</td>
    <td style="text-align:center">$50</td>
    </tr>
    <tr>
    <td style="text-align:center">2012-06-30</td>
    <td style="text-align:center">$27</td>
    </tr>
    <tr>
    <td style="text-align:center">2012-03-31</td>
    <td style="text-align:center">$30</td>
    </tr>
    <tr>
    <td style="text-align:center">2011-12-31</td>
    <td style="text-align:center">$39</td>
    </tr>
    <tr>
    <td style="text-align:center">2011-09-30</td>
    <td style="text-align:center">$58</td>
    </tr>
    <tr>
    <td style="text-align:center">2011-06-30</td>
    <td style="text-align:center">$58</td>
    </tr>
    <tr>
    <td style="text-align:center">2011-03-31</td>
    <td style="text-align:center">$49</td>
    </tr>
    <tr>
    <td style="text-align:center">2010-12-31</td>
    <td style="text-align:center">$36</td>
    </tr>
    <tr>
    <td style="text-align:center">2010-09-30</td>
    <td style="text-align:center">$31</td>
    </tr>
    <tr>
    <td style="text-align:center">2010-06-30</td>
    <td style="text-align:center">$28</td>
    </tr>
    <tr>
    <td style="text-align:center">2010-03-31</td>
    <td style="text-align:center">$21</td>
    </tr>
    <tr>
    <td style="text-align:center">2009-12-31</td>
    <td style="text-align:center"></td>
    </tr>
    <tr>
    <td style="text-align:center">2009-09-30</td>
    <td style="text-align:center">$46</td>
    </tr>
    <tr>
    <td style="text-align:center">2009-06-30</td>
    <td style="text-align:center">$27</td>
    </tr>
    </tbody>
    </table>
    </div>
    </div>
    <div style="background-color:#fff; margin: 0px 0px 20px 0px; padding:5px 50px 5px 10px; border:1px solid #dfdfdf;">
    <table class="historical_data_table table">
    <thead>
    <tr>
    <th style="text-align:center">Sector</th>
    <th style="text-align:center">Industry</th>
    <th style="text-align:center">Market Cap</th>
    <th style="text-align:center">Revenue</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:center"><a href="https://www.macrotrends.net/stocks/sector/5/auto-tires-trucks">Auto/Tires/Trucks</a></td>
    <td style="text-align:center"><a href="https://www.macrotrends.net/stocks/industry/7/">Auto Manufacturers - Domestic</a></td>
    <td style="text-align:center">$549.575B</td>
    <td style="text-align:center">$53.823B</td>
    </tr>
    <tr>
    <td colspan="4" style="padding:15px;">
    <span>Tesla is the market leader in battery-powered electric car sales in the United States, with roughly 70% market share. The company's flagship Model 3 is the best-selling EV model in the United States. Tesla, which has managed to garner the reputation of a gold standard over the years, is now a far bigger entity that what it started off since its IPO in 2010, with its market cap crossing $1 trillion for the first time in October 2021.? The EV king's market capitalization is more than the combined value of legacy automakers including Toyota, Volkswagen, Daimler, General Motors and Ford.Over the years, Tesla has shifted from developing niche products for affluent buyers to making more affordable EVs for the masses. The firm's three-pronged business model approach of direct sales, servicing, and charging its EVs sets it apart from other carmakers. Tesla, which is touted as the clean energy revolutionary automaker, is much more than just a car manufacturer.</span>
    </td>
    </tr>
    </tbody>
    </table>
    </div>
    <div style="background-color:#fff; margin: 20px 0px 30px 0px; padding:5px 50px 5px 10px; border:1px solid #dfdfdf;">
    <table class="historical_data_table table">
    <thead>
    <tr>
    <th style="text-align:center; width:40%;">Stock Name</th>
    <th style="text-align:center; width:20%;">Country</th>
    <th style="text-align:center; width:20%;">Market Cap</th>
    <th style="text-align:center; width:20%;">PE Ratio</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/GM/general-motors/revenue">General Motors (GM)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$53.930B</td>
    <td style="text-align:center">5.56</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/F/ford-motor/revenue">Ford Motor (F)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$52.668B</td>
    <td style="text-align:center">8.09</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/HOG/harley-davidson/revenue">Harley-Davidson (HOG)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$6.762B</td>
    <td style="text-align:center">9.56</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/PII/polaris/revenue">Polaris (PII)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$6.267B</td>
    <td style="text-align:center">11.86</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/IAA/iaa/revenue">IAA (IAA)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$5.134B</td>
    <td style="text-align:center">16.40</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/FSR/fisker/revenue">Fisker (FSR)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$2.261B</td>
    <td style="text-align:center">0.00</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/LEV/lion-electric/revenue">Lion Electric (LEV)</a></td>
    <td style="text-align:center">Canada</td>
    <td style="text-align:center">$0.551B</td>
    <td style="text-align:center">0.00</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/VLTA/volta/revenue">Volta (VLTA)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$0.071B</td>
    <td style="text-align:center">0.00</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/BRDS/bird-global/revenue">Bird Global (BRDS)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$0.054B</td>
    <td style="text-align:center">0.00</td>
    </tr>
    <tr>
    <td style="text-align:left"><a href="/stocks/charts/ZEV/lightning-emotors/revenue">Lightning EMotors (ZEV)</a></td>
    <td style="text-align:center">United States</td>
    <td style="text-align:center">$0.043B</td>
    <td style="text-align:center">0.00</td>
    </tr>
    </tbody>
    </table>
    </div>
    <div>
    <!-- Partner Center Ad Unit -->
    <div id="IC_728x214_1" style="width:728px; height:214px; margin-left:30px;">
    </div>
    </div>
    </div>
    <div id="right_sidebar">
    <!--<a href="/stocks/stock-screener" style="text-decoration:none; color: #fff; ">
    					<div style="margin:0px; padding: 20px; width:300px; background-color: #01579b; min-height:150px; text-align:center;">
    
    						<h2 style="font-weight:600;">Try our new<br />stock screener!</h2></a>
    
    					</div>
    				</a>-->
    <!--<div style="margin-top:0px; min-height:250px;">
    
    					<script src='//ads.investingchannel.com/adtags/Macrotrends/fundamentalanalysis/300x600.js?zhpos=300_2&multi_size=false' type='text/javascript' charset='utf-8'></script>
    
    				</div>-->
    <div style="margin-top:0px; min-height:250px;">
    <div id="ic_300x250_1">
    </div>
    </div>
    <div id="sticky_ad_right" style="margin-top:30px; height:1000px;">
    <script id="dianomi_context_script" src="https://www.dianomi.com/js/contextfeed.js" type="text/javascript"></script>
    <div class="dianomi_context" data-dianomi-context-id="743"></div>
    <!-- <div id="IC_D_300x250_BCC"></div>-->
    <!--Smartad # 2981: Macrotrends - 300x670 Right Rail-->
    <iframe height="670" id="dianomi_sidebar" scrolling="NO" src="//www.dianomi.com/smartads.epl?id=4059" style="width: 300px; border: none; overflow: hidden;" width="300"></iframe>
    <div id="IC_D_300x250_BCC"></div>
    </div>
    </div>
    </div>
    </div>
    <!--This is the div for the IC OOP ad-->
    <div id="oopDivTag_1" style="width:1px;height:1px;"></div>
    <footer class="footer">
    <span>© 2010-2022 Macrotrends LLC</span>  |  
    		  <a href="/terms">Terms of Service</a>
    		    |  
    		  <a href="/privacy">Privacy Policy</a>  |  
    		  <a href="mailto:%69n%66o@%6Dac%72otrends%2En%65t">Contact Us</a>  |  
    		  <a href="/ccpa">Do Not Sell My Personal Information</a>
    <br/>
    <span>Fundamental data from </span><a href="https://www.zacksdata.com" rel="nofollow" target="_blank">Zacks Investment Research, Inc.</a>
    </footer>
    <div aria-hidden="true" aria-labelledby="exampleModalLabel" class="modal" id="smallWidthModal1" role="dialog" tabindex="-1">
    <div class="modal-dialog modal-lg">
    <div class="modal-content">
    <div class="modal-body">
    <div class="modal_title"><h2><strong>We Need Your Support!</strong></h2></div>
    <p>Backlinks from other websites are the lifeblood of our site and a primary source of new traffic.</p><p>
    </p><p>If you use our chart images on your site or blog, we ask that you provide attribution via a "dofollow" link back to this page.  We have provided a few examples below that you can copy and paste to your site:</p>
    <br/>
    <table class="table">
    <thead>
    <tr>
    <th>Link Preview</th>
    <th>HTML Code (Click to Copy)</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><a>Tesla Revenue 2010-2022 | TSLA</a></td>
    <td><input class="modal_link" size="60" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Tesla Revenue 2010-2022 | TSLA&lt;/a&gt;"/></td>
    </tr>
    <tr>
    <td><a>Macrotrends</a></td>
    <td><input class="modal_link" size="60" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Macrotrends&lt;/a&gt;"/></td>
    </tr>
    <tr>
    <td><a>Source</a></td>
    <td><input class="modal_link" size="60" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Source&lt;/a&gt;"/></td>
    </tr>
    </tbody>
    </table>
    <br/>
    <p style="text-align:center">Your image export is now complete.  Please check your download folder. </p>
    </div>
    <div class="modal-footer">
    <button class="btn btn-primary" data-dismiss="modal" type="button">Close Window</button>
    </div>
    </div>
    </div>
    </div>
    <div aria-hidden="true" aria-labelledby="exampleModalLabel" class="modal" id="smallWidthModal2" role="dialog" tabindex="-1">
    <div class="modal-dialog modal-lg">
    <div class="modal-content">
    <div class="modal-body">
    <div class="modal_title"><h2><strong>We Need Your Support!</strong></h2></div>
    <p>Backlinks from other websites are the lifeblood of our site and a primary source of new traffic.</p><p>
    </p><p>If you use our datasets on your site or blog, we ask that you provide attribution via a "dofollow" link back to this page.  We have provided a few examples below that you can copy and paste to your site:</p>
    <br/>
    <table class="table">
    <thead>
    <tr>
    <th>Link Preview</th>
    <th>HTML Code (Click to Copy)</th>
    </tr>
    </thead>
    <tbody>
    <tr>
    <td><a>Tesla Revenue 2010-2022 | TSLA</a></td>
    <td><input class="modal_link" size="50" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Tesla Revenue 2010-2022 | TSLA&lt;/a&gt;"/></td>
    </tr>
    <tr>
    <td><a>Macrotrends</a></td>
    <td><input class="modal_link" size="50" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Macrotrends&lt;/a&gt;"/></td>
    </tr>
    <tr>
    <td><a>Source</a></td>
    <td><input class="modal_link" size="50" type="text" value="&lt;a href='https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue'&gt;Source&lt;/a&gt;"/></td>
    </tr>
    </tbody>
    </table>
    <br/>
    <p style="text-align:center">Your data export is now complete.  Please check your download folder. </p>
    </div>
    <div class="modal-footer">
    <button class="btn btn-primary" data-dismiss="modal" type="button">Close Window</button>
    </div>
    </div>
    </div>
    </div>
    <script type="text/javascript">
    	$.typeahead({
    		input: '.js-typeahead',
    		minLength: 1,
    		filter: false,  //Disables typahead filter to just show everything in the results from the database
    		debug: false,
    		highlight: true,
    		maxItem: 10,
    		dynamic: true,
    		delay: 200,
    		searchOnFocus: true,
    		backdrop: {
    			"background-color": "#fff"
    		},
    		href: "{{url}}",
    		emptyTemplate: "no result for {{query}}",
    		display: ["name"],
    		source: {
    			users: {
    				ajax: {
    					url: '/assets/php/all_pages_query.php',
    					data: {
    						q: '{{query}}'
    					}
    				}
    			}
    		}
    	});
    </script>
    <script>
    
    	// /*! js-cookie v3.0.0-rc.1 | MIT */
    	// !function(e,t){"object"==typeof exports&&"undefined"!=typeof module?module.exports=t():"function"==typeof define&&define.amd?define(t):(e=e||self,function(){var n=e.Cookies,r=e.Cookies=t();r.noConflict=function(){return e.Cookies=n,r}}())}(this,function(){"use strict";function e(e){for(var t=1;t<arguments.length;t++){var n=arguments[t];for(var r in n)e[r]=n[r]}return e}var t={read:function(e){return e.replace(/(%[\dA-F]{2})+/gi,decodeURIComponent)},write:function(e){return encodeURIComponent(e).replace(/%(2[346BF]|3[AC-F]|40|5[BDE]|60|7[BCD])/g,decodeURIComponent)}};return function n(r,o){function i(t,n,i){if("undefined"!=typeof document){"number"==typeof(i=e({},o,i)).expires&&(i.expires=new Date(Date.now()+864e5*i.expires)),i.expires&&(i.expires=i.expires.toUTCString()),t=encodeURIComponent(t).replace(/%(2[346B]|5E|60|7C)/g,decodeURIComponent).replace(/[()]/g,escape),n=r.write(n,t);var c="";for(var u in i)i[u]&&(c+="; "+u,!0!==i[u]&&(c+="="+i[u].split(";")[0]));return document.cookie=t+"="+n+c}}return Object.create({set:i,get:function(e){if("undefined"!=typeof document&&(!arguments.length||e)){for(var n=document.cookie?document.cookie.split("; "):[],o={},i=0;i<n.length;i++){var c=n[i].split("="),u=c.slice(1).join("=");'"'===u[0]&&(u=u.slice(1,-1));try{var f=t.read(c[0]);if(o[f]=r.read(u,f),e===f)break}catch(e){}}return e?o[e]:o}},remove:function(t,n){i(t,"",e({},n,{expires:-1}))},withAttributes:function(t){return n(this.converter,e({},this.attributes,t))},withConverter:function(t){return n(e({},this.converter,t),this.attributes)}},{attributes:{value:Object.freeze(o)},converter:{value:Object.freeze(r)}})}(t,{path:"/"})});
    
    			
    	// // Cookie Settings
    	// var maxCookieValue = 4, initCookie = 1, expirationDays = 1;
    	// var cookieName = "session_pageviews";
    	// var getCookie = Cookies.get(cookieName);
    
    	// // Under the Hood
    	// if (getCookie == null) {
    		// Cookies.set(cookieName, initCookie, { expires: expirationDays });
    		// console.log('Cookie set to value 1');
    		// $( "#ic_video_ad" ).append( "<div id=\"IC_D_3x6\" style=\"margin:30px;\"></div>" );
    	// } else {
    		// if (getCookie >= initCookie && getCookie < maxCookieValue) {
    			// getCookie++;
    			// Cookies.set(cookieName, getCookie, { expires: expirationDays });
    			// console.log('Cookie incremented. New value is ' + getCookie);
    			// $( "#ic_video_ad" ).append( "<div id=\"IC_D_3x6\" style=\"margin:30px;\"></div>" );
    		// }
    		// else if (getCookie >= maxCookieValue && getCookie < 7) {
    			// getCookie++;
    			// Cookies.set(cookieName, getCookie, { expires: expirationDays });
    			// console.log('Cookie max allowed value reached. No video ads showing. New value is ' + getCookie);
    			// //Cookies.remove(cookieName);
    			// // if cookie is equal with the number you've set, then do something
    			// // hide an element, delete the cookie etc...
    		// }
    		// else if (getCookie >= 7) {
    			// Cookies.remove(cookieName);
    			// // if cookie is equal with the number you've set, then do something
    			// // hide an element, delete the cookie etc...
    		// }	
    	// }
    
    </script>
    <script>
    
    
    
    
    		
    
    $(document).ready(function() {
    	
    	var user_data = '171.76.81.154';	var country_code = 'United States';
    	$.post('https://www.macrotrends.net/assets/php/user_frequency_tracking.php', {user_ip: user_data, user_country: country_code}); 
    
    	// Selects all of the text in the chart export window when clicked
    	$(".modal_link").focus(function() {
    		var $this = $(this);
    		$this.select();
    
    		// Work around Chrome's little problem
    		$this.mouseup(function() {
    			// Prevent further mouseup intervention
    			$this.unbind("mouseup");
    			return false;
    		});
    	});	
    	
    	
    	$('[data-toggle="tooltip"]').tooltip();
    	
        $('.statement_type_select').select2({
    	
    	theme: "classic",
    	minimumResultsForSearch: 20
    	
    	});
    
        $('.frequency_select').select2({
    	
    	theme: "classic",
    	minimumResultsForSearch: 20
    	
    	});
    	
    	
    });
    
    $( "#compareStocks" ).click(function() {
    	
    	
    	window.location.href = '/stocks/stock-comparison?s=revenue&axis=single&comp=TSLA';
    	
    	
    });
    
    $( "#chartExport" ).click(function() {
    	
    		window.$('#smallWidthModal1').modal();
    
    		//Turn off scroll bar for image export
    		chart.chartScrollbarSettings.enabled = false;
    		chart.validateNow(); 
    		
    		
    		chart.export.capture({},function() {
    			this.toPNG({},function(data) {
    				// Download the image to the browser
    				this.download( data, "image/png", "TSLA-revenue-2022-12-09-macrotrends.png" );
    				
    				});
    
    		//Turn scroll bar back on again
    		chart.chartScrollbarSettings.enabled = true;
    		chart.validateNow(); 
    				
    	});
    
    });
    
    $( ".statement_type_select" ).change(function() {
      
      window.location.href = 'https://testing.macrotrends.net/assets/php/income_statement_testing.php?t=ZEV&type=' + this.value + '&freq=Q';
    
    });
    
    $( ".frequency_select" ).change(function() {
      
      window.location.href = '/assets/php/new_chart_page.php?t=ZEV&type=revenue&freq=' + this.value;
    
    });
    
    </script>
    <!--<div class="modal" id="contribute_modal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="false">
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-body" style="margin:20px 40px 20px 40px; text-align:left;font-size:18px;">
    	  	  
    
    
    <div class="row">
    
    <div class="col-xs-6">
    
    <script src="https://donorbox.org/widget.js" paypalExpress="true"></script><iframe src="https://donorbox.org/embed/macrotrends-donations?hide_donation_meter=true" height="685px" width="100%" style="max-width:500px; min-width:310px; max-height:none!important" seamless="seamless" name="donorbox" frameborder="0" scrolling="no" allowpaymentrequest></iframe>
    
    </div>
    
    <div class="col-xs-6">
    
    		<div class="modal_title"><h1><strong>We Need Your Support!</strong></h1></div>
    
    		<p><strong>Macrotrends has been subscription-free since 2010 and we want to keep it that way.</strong></p>
    
    <p>Our goal has always been to serve as an easily accessible, high quality source of investment research for both professionals and amateurs alike.</p>
    
    <p>Any amount that you can contribute will help ensure we can keep the site completely free for many years to come.</p>
    
    <p style="margin-top:20px;">Regards,</p>
    <p>The Macrotrends Team</p>
    
    </div>
    
    </div>
    
    </div>
    
          <div class="modal-footer" style="text-align:center;">
            <button type="button" class="btn btn-success" data-dismiss="modal">Maybe Next Time...</button>
          </div>
        </div>
      </div>
    </div>	
    
    
    <script src="/ads.js" type="text/javascript"></script>
    
    <script>
    
    $(document).ready(function() {
    	
    	var botPattern = "(googlebot\/|Googlebot-Mobile|Googlebot-Image|Google favicon|Mediapartners-Google|bingbot|slurp|java|wget|curl|Commons-HttpClient|Python-urllib|libwww|httpunit|nutch|phpcrawl|msnbot|jyxobot|FAST-WebCrawler|FAST Enterprise Crawler|biglotron|teoma|convera|seekbot|gigablast|exabot|ngbot|ia_archiver|GingerCrawler|webmon |httrack|webcrawler|grub.org|UsineNouvelleCrawler|antibot|netresearchserver|speedy|fluffy|bibnum.bnf|findlink|msrbot|panscient|yacybot|AISearchBot|IOI|ips-agent|tagoobot|MJ12bot|dotbot|woriobot|yanga|buzzbot|mlbot|yandexbot|purebot|Linguee Bot|Voyager|CyberPatrol|voilabot|baiduspider|citeseerxbot|spbot|twengabot|postrank|turnitinbot|scribdbot|page2rss|sitebot|linkdex|Adidxbot|blekkobot|ezooms|dotbot|Mail.RU_Bot|discobot|heritrix|findthatfile|europarchive.org|NerdByNature.Bot|sistrix crawler|ahrefsbot|Aboundex|domaincrawler|wbsearchbot|summify|ccbot|edisterbot|seznambot|ec2linkfinder|gslfbot|aihitbot|intelium_bot|facebookexternalhit|yeti|RetrevoPageAnalyzer|lb-spider|sogou|lssbot|careerbot|wotbox|wocbot|ichiro|DuckDuckBot|lssrocketcrawler|drupact|webcompanycrawler|acoonbot|openindexspider|gnam gnam spider|web-archive-net.com.bot|backlinkcrawler|coccoc|integromedb|content crawler spider|toplistbot|seokicks-robot|it2media-domain-crawler|ip-web-crawler.com|siteexplorer.info|elisabot|proximic|changedetection|blexbot|arabot|WeSEE:Search|niki-bot|CrystalSemanticsBot|rogerbot|360Spider|psbot|InterfaxScanBot|Lipperhey SEO Service|CC Metadata Scaper|g00g1e.net|GrapeshotCrawler|urlappendbot|brainobot|fr-crawler|binlar|SimpleCrawler|Livelapbot|Twitterbot|cXensebot|smtbot|bnf.fr_bot|A6-Indexer|ADmantX|Facebot|Twitterbot|OrangeBot|memorybot|AdvBot|MegaIndex|SemanticScholarBot|ltx71|nerdybot|xovibot|BUbiNG|Qwantify|archive.org_bot|Applebot|TweetmemeBot|crawler4j|findxbot|SemrushBot|yoozBot|lipperhey|y!j-asr|Domain Re-Animator Bot|AddThis)";
    
    	var re = new RegExp(botPattern, 'i');
    
    	if (re.test(navigator.userAgent)) {
    		
    	} else {
    		
    		//Check to see whether they are running an ad blocker
    		if(document.getElementById('12mORwMnaEkJXlxz')){
    		  var ad_blocker = 'N';
    		} else {
    		  var ad_blocker = 'Y';
    		}
    
    		$.post('https://api.ipstack.com/check?access_key=14fe63e83d5cfefa0b3d4cec498479ba&output=json&fields=ip,continent_name,country_name,region_name,city', 
    		function(ip_data){
    			
    			$.post('https://www.macrotrends.net/assets/php/page_view_tracking.php', {ip: ip_data.ip,continent: ip_data.continent_name, country: ip_data.country_name, state: ip_data.region_name, city: ip_data.city, screen_width: screen.width, ads: ad_blocker, page_type: 'stock'}, 
    				function(data){
    					/*					
    					if(data % 20 === 0) {
    						
    						//$('#contribute_modal').modal();
    						
    					}
    					*/
    				});
    		
    		});
    
    
    	}
    	
    
    });
    
    
    $.post('https://api.ipstack.com/check?access_key=14fe63e83d5cfefa0b3d4cec498479ba&output=json&fields=ip,continent_name,country_name,region_name,city', 
    function(ip_data){
    	
    	$(".contribute_user_id").val(ip_data.ip);
    	
    });
    
    $( ".donate_buttons" ).click(function() {
      
    	var payment = $(this).attr("value");
    
    	$.post('https://api.ipstack.com/check?access_key=14fe63e83d5cfefa0b3d4cec498479ba&output=json&fields=ip,continent_name,country_name,region_name,city', 
    		function(ip_data){
    					
    		$.post('https://www.macrotrends.net/assets/php/page_view_tracking.php', {ip: ip_data.ip, paid: payment}); 
    	
    	});
    		 
    });
    
    </script>
    
    -->
    <script type="text/javascript">
    var clicky_site_ids = clicky_site_ids || [];
    clicky_site_ids.push(100827248);
    (function() {
      var s = document.createElement('script');
      s.type = 'text/javascript';
      s.async = true;
      s.src = '//static.getclicky.com/js';
      ( document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0] ).appendChild( s );
    })();
    </script>
    <noscript><p><img alt="Clicky" height="1" src="//in.getclicky.com/100827248ns.gif" width="1"/></p></noscript>
    <!-- This site is converting visitors into subscribers and customers with OptinMonster - https://optinmonster.com -->
    <!-- <script type="text/javascript" src="https://a.omappapi.com/app/js/api.min.js" data-account="6392" data-user="15772" async></script> -->
    <!-- / OptinMonster -->
    </body>
    </html>



Using `BeautifulSoup` or the `read_html` function extract the table with `Tesla Revenue` and store it into a dataframe named `tesla_revenue`. The dataframe should have columns `Date` and `Revenue`.


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1


```

</details>



```python
tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])

for row in soup.find("tbody").find_all("tr"):
    col = row.find_all("td")
    date = col[0].text
    revenue = col[1].text
    

    tesla_revenue = tesla_revenue.append({"Date":date, "Revenue":revenue}, ignore_index = True)
    print(tesla_revenue)
```

       Date  Revenue
    0  2021  $53,823
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
    5  2016   $7,000
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
    5  2016   $7,000
    6  2015   $4,046
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
    5  2016   $7,000
    6  2015   $4,046
    7  2014   $3,198
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
    5  2016   $7,000
    6  2015   $4,046
    7  2014   $3,198
    8  2013   $2,013
       Date  Revenue
    0  2021  $53,823
    1  2020  $31,536
    2  2019  $24,578
    3  2018  $21,461
    4  2017  $11,759
    5  2016   $7,000
    6  2015   $4,046
    7  2014   $3,198
    8  2013   $2,013
    9  2012     $413
        Date  Revenue
    0   2021  $53,823
    1   2020  $31,536
    2   2019  $24,578
    3   2018  $21,461
    4   2017  $11,759
    5   2016   $7,000
    6   2015   $4,046
    7   2014   $3,198
    8   2013   $2,013
    9   2012     $413
    10  2011     $204
        Date  Revenue
    0   2021  $53,823
    1   2020  $31,536
    2   2019  $24,578
    3   2018  $21,461
    4   2017  $11,759
    5   2016   $7,000
    6   2015   $4,046
    7   2014   $3,198
    8   2013   $2,013
    9   2012     $413
    10  2011     $204
    11  2010     $117
        Date  Revenue
    0   2021  $53,823
    1   2020  $31,536
    2   2019  $24,578
    3   2018  $21,461
    4   2017  $11,759
    5   2016   $7,000
    6   2015   $4,046
    7   2014   $3,198
    8   2013   $2,013
    9   2012     $413
    10  2011     $204
    11  2010     $117
    12  2009     $112


Execute the following line to remove the comma and dollar sign from the `Revenue` column. 



```python
 tesla_revenue["Revenue"] = tesla_revenue['Revenue'].str.replace(',|\$',"")
```

    /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages/ipykernel_launcher.py:1: FutureWarning:
    
    The default value of regex will change from True to False in a future version.
    


Execute the following lines to remove an null or empty strings in the Revenue column.



```python
tesla_revenue.dropna(inplace=True)

tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
```

Display the last 5 row of the `tesla_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python
tesla_revenue.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>2013</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2012</td>
      <td>413</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2011</td>
      <td>204</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2010</td>
      <td>117</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2009</td>
      <td>112</td>
    </tr>
  </tbody>
</table>
</div>



## Question 3: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is `GME`.



```python
gamestop = yf.Ticker('GME')
```

Using the ticker object and the function `history` extract stock information and save it in a dataframe named `gme_data`. Set the `period` parameter to `max` so we get information for the maximum amount of time.



```python
gme_data = gamestop.history(period = 'max')
gme_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2002-02-13</th>
      <td>1.620128</td>
      <td>1.693350</td>
      <td>1.603296</td>
      <td>1.691666</td>
      <td>76216000</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2002-02-14</th>
      <td>1.712707</td>
      <td>1.716074</td>
      <td>1.670626</td>
      <td>1.683251</td>
      <td>11021600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2002-02-15</th>
      <td>1.683250</td>
      <td>1.687458</td>
      <td>1.658001</td>
      <td>1.674834</td>
      <td>8389600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2002-02-19</th>
      <td>1.666418</td>
      <td>1.666418</td>
      <td>1.578047</td>
      <td>1.607504</td>
      <td>7410400</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2002-02-20</th>
      <td>1.615920</td>
      <td>1.662209</td>
      <td>1.603296</td>
      <td>1.662209</td>
      <td>6892800</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-09-18</th>
      <td>17.990000</td>
      <td>18.100000</td>
      <td>17.350000</td>
      <td>17.549999</td>
      <td>3694600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-19</th>
      <td>17.590000</td>
      <td>17.639999</td>
      <td>17.129999</td>
      <td>17.520000</td>
      <td>2584200</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-20</th>
      <td>17.629999</td>
      <td>17.930000</td>
      <td>17.450001</td>
      <td>17.520000</td>
      <td>2129800</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-21</th>
      <td>17.280001</td>
      <td>17.320000</td>
      <td>16.650000</td>
      <td>17.020000</td>
      <td>2910700</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2023-09-22</th>
      <td>17.180000</td>
      <td>17.350000</td>
      <td>17.000000</td>
      <td>17.180000</td>
      <td>2100300</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5440 rows × 7 columns</p>
</div>



**Reset the index** using the `reset_index(inplace=True)` function on the gme_data DataFrame and display the first five rows of the `gme_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.



```python
gme_data.reset_index(inplace=True)
gme_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002-02-13</td>
      <td>1.620128</td>
      <td>1.693350</td>
      <td>1.603296</td>
      <td>1.691666</td>
      <td>76216000</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002-02-14</td>
      <td>1.712707</td>
      <td>1.716074</td>
      <td>1.670626</td>
      <td>1.683251</td>
      <td>11021600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002-02-15</td>
      <td>1.683250</td>
      <td>1.687458</td>
      <td>1.658001</td>
      <td>1.674834</td>
      <td>8389600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002-02-19</td>
      <td>1.666418</td>
      <td>1.666418</td>
      <td>1.578047</td>
      <td>1.607504</td>
      <td>7410400</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002-02-20</td>
      <td>1.615920</td>
      <td>1.662209</td>
      <td>1.603296</td>
      <td>1.662209</td>
      <td>6892800</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Question 4: Use Webscraping to Extract GME Revenue Data


Use the `requests` library to download the webpage https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html. Save the text of the response as a variable named `html_data`.



```python
url1 = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html'

html_data1 = requests.get(url1).text
```

Parse the html data using `beautiful_soup`.



```python
gme_data_bs = BeautifulSoup(html_data1)
```

Using `BeautifulSoup` or the `read_html` function extract the table with `GameStop Revenue` and store it into a dataframe named `gme_revenue`. The dataframe should have columns `Date` and `Revenue`. Make sure the comma and dollar sign is removed from the `Revenue` column using a method similar to what you did in Question 2.


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1


```

</details>



```python
gme_revenue = pd.DataFrame(columns=["Date", "Revenue"])

for row in gme_data_bs.find("tbody").find_all("tr"):
    col = row.find_all("td")
    date = col[0].text
    revenue = col[1].text
    

    gme_revenue = gme_revenue.append({"Date":date, "Revenue":revenue}, ignore_index = True)
    print(gme_revenue)
```

       Date Revenue
    0  2020  $6,466
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
    5  2015  $9,296
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
    5  2015  $9,296
    6  2014  $9,040
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
    5  2015  $9,296
    6  2014  $9,040
    7  2013  $8,887
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
    5  2015  $9,296
    6  2014  $9,040
    7  2013  $8,887
    8  2012  $9,551
       Date Revenue
    0  2020  $6,466
    1  2019  $8,285
    2  2018  $8,547
    3  2017  $7,965
    4  2016  $9,364
    5  2015  $9,296
    6  2014  $9,040
    7  2013  $8,887
    8  2012  $9,551
    9  2011  $9,474
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
    11  2009  $8,806
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
    11  2009  $8,806
    12  2008  $7,094
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
    11  2009  $8,806
    12  2008  $7,094
    13  2007  $5,319
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
    11  2009  $8,806
    12  2008  $7,094
    13  2007  $5,319
    14  2006  $3,092
        Date Revenue
    0   2020  $6,466
    1   2019  $8,285
    2   2018  $8,547
    3   2017  $7,965
    4   2016  $9,364
    5   2015  $9,296
    6   2014  $9,040
    7   2013  $8,887
    8   2012  $9,551
    9   2011  $9,474
    10  2010  $9,078
    11  2009  $8,806
    12  2008  $7,094
    13  2007  $5,319
    14  2006  $3,092
    15  2005  $1,843


Display the last five rows of the `gme_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python
gme_revenue["Revenue"] = gme_revenue['Revenue'].str.replace(',|\$',"")
gme_revenue.dropna(inplace=True)

gme_revenue = gme_revenue[gme_revenue['Revenue'] != ""]
gme_revenue.tail()
```

    /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages/ipykernel_launcher.py:1: FutureWarning:
    
    The default value of regex will change from True to False in a future version.
    





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>2009</td>
      <td>8806</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2008</td>
      <td>7094</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2007</td>
      <td>5319</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2006</td>
      <td>3092</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2005</td>
      <td>1843</td>
    </tr>
  </tbody>
</table>
</div>



## Question 5: Plot Tesla Stock Graph


Use the `make_graph` function to graph the Tesla Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(tesla_data, tesla_revenue, 'Tesla')`. Note the graph will only show data upto June 2021.



```python
make_graph(tesla_data, tesla_revenue, 'Tesla')
```


<div>                            <div id="1984855c-8134-4daf-8421-857f0cdd4c99" class="plotly-graph-div" style="height:900px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("1984855c-8134-4daf-8421-857f0cdd4c99")) {                    Plotly.newPlot(                        "1984855c-8134-4daf-8421-857f0cdd4c99",                        [{"name":"Share Price","x":["2010-06-29T00:00:00","2010-06-30T00:00:00","2010-07-01T00:00:00","2010-07-02T00:00:00","2010-07-06T00:00:00","2010-07-07T00:00:00","2010-07-08T00:00:00","2010-07-09T00:00:00","2010-07-12T00:00:00","2010-07-13T00:00:00","2010-07-14T00:00:00","2010-07-15T00:00:00","2010-07-16T00:00:00","2010-07-19T00:00:00","2010-07-20T00:00:00","2010-07-21T00:00:00","2010-07-22T00:00:00","2010-07-23T00:00:00","2010-07-26T00:00:00","2010-07-27T00:00:00","2010-07-28T00:00:00","2010-07-29T00:00:00","2010-07-30T00:00:00","2010-08-02T00:00:00","2010-08-03T00:00:00","2010-08-04T00:00:00","2010-08-05T00:00:00","2010-08-06T00:00:00","2010-08-09T00:00:00","2010-08-10T00:00:00","2010-08-11T00:00:00","2010-08-12T00:00:00","2010-08-13T00:00:00","2010-08-16T00:00:00","2010-08-17T00:00:00","2010-08-18T00:00:00","2010-08-19T00:00:00","2010-08-20T00:00:00","2010-08-23T00:00:00","2010-08-24T00:00:00","2010-08-25T00:00:00","2010-08-26T00:00:00","2010-08-27T00:00:00","2010-08-30T00:00:00","2010-08-31T00:00:00","2010-09-01T00:00:00","2010-09-02T00:00:00","2010-09-03T00:00:00","2010-09-07T00:00:00","2010-09-08T00:00:00","2010-09-09T00:00:00","2010-09-10T00:00:00","2010-09-13T00:00:00","2010-09-14T00:00:00","2010-09-15T00:00:00","2010-09-16T00:00:00","2010-09-17T00:00:00","2010-09-20T00:00:00","2010-09-21T00:00:00","2010-09-22T00:00:00","2010-09-23T00:00:00","2010-09-24T00:00:00","2010-09-27T00:00:00","2010-09-28T00:00:00","2010-09-29T00:00:00","2010-09-30T00:00:00","2010-10-01T00:00:00","2010-10-04T00:00:00","2010-10-05T00:00:00","2010-10-06T00:00:00","2010-10-07T00:00:00","2010-10-08T00:00:00","2010-10-11T00:00:00","2010-10-12T00:00:00","2010-10-13T00:00:00","2010-10-14T00:00:00","2010-10-15T00:00:00","2010-10-18T00:00:00","2010-10-19T00:00:00","2010-10-20T00:00:00","2010-10-21T00:00:00","2010-10-22T00:00:00","2010-10-25T00:00:00","2010-10-26T00:00:00","2010-10-27T00:00:00","2010-10-28T00:00:00","2010-10-29T00:00:00","2010-11-01T00:00:00","2010-11-02T00:00:00","2010-11-03T00:00:00","2010-11-04T00:00:00","2010-11-05T00:00:00","2010-11-08T00:00:00","2010-11-09T00:00:00","2010-11-10T00:00:00","2010-11-11T00:00:00","2010-11-12T00:00:00","2010-11-15T00:00:00","2010-11-16T00:00:00","2010-11-17T00:00:00","2010-11-18T00:00:00","2010-11-19T00:00:00","2010-11-22T00:00:00","2010-11-23T00:00:00","2010-11-24T00:00:00","2010-11-26T00:00:00","2010-11-29T00:00:00","2010-11-30T00:00:00","2010-12-01T00:00:00","2010-12-02T00:00:00","2010-12-03T00:00:00","2010-12-06T00:00:00","2010-12-07T00:00:00","2010-12-08T00:00:00","2010-12-09T00:00:00","2010-12-10T00:00:00","2010-12-13T00:00:00","2010-12-14T00:00:00","2010-12-15T00:00:00","2010-12-16T00:00:00","2010-12-17T00:00:00","2010-12-20T00:00:00","2010-12-21T00:00:00","2010-12-22T00:00:00","2010-12-23T00:00:00","2010-12-27T00:00:00","2010-12-28T00:00:00","2010-12-29T00:00:00","2010-12-30T00:00:00","2010-12-31T00:00:00","2011-01-03T00:00:00","2011-01-04T00:00:00","2011-01-05T00:00:00","2011-01-06T00:00:00","2011-01-07T00:00:00","2011-01-10T00:00:00","2011-01-11T00:00:00","2011-01-12T00:00:00","2011-01-13T00:00:00","2011-01-14T00:00:00","2011-01-18T00:00:00","2011-01-19T00:00:00","2011-01-20T00:00:00","2011-01-21T00:00:00","2011-01-24T00:00:00","2011-01-25T00:00:00","2011-01-26T00:00:00","2011-01-27T00:00:00","2011-01-28T00:00:00","2011-01-31T00:00:00","2011-02-01T00:00:00","2011-02-02T00:00:00","2011-02-03T00:00:00","2011-02-04T00:00:00","2011-02-07T00:00:00","2011-02-08T00:00:00","2011-02-09T00:00:00","2011-02-10T00:00:00","2011-02-11T00:00:00","2011-02-14T00:00:00","2011-02-15T00:00:00","2011-02-16T00:00:00","2011-02-17T00:00:00","2011-02-18T00:00:00","2011-02-22T00:00:00","2011-02-23T00:00:00","2011-02-24T00:00:00","2011-02-25T00:00:00","2011-02-28T00:00:00","2011-03-01T00:00:00","2011-03-02T00:00:00","2011-03-03T00:00:00","2011-03-04T00:00:00","2011-03-07T00:00:00","2011-03-08T00:00:00","2011-03-09T00:00:00","2011-03-10T00:00:00","2011-03-11T00:00:00","2011-03-14T00:00:00","2011-03-15T00:00:00","2011-03-16T00:00:00","2011-03-17T00:00:00","2011-03-18T00:00:00","2011-03-21T00:00:00","2011-03-22T00:00:00","2011-03-23T00:00:00","2011-03-24T00:00:00","2011-03-25T00:00:00","2011-03-28T00:00:00","2011-03-29T00:00:00","2011-03-30T00:00:00","2011-03-31T00:00:00","2011-04-01T00:00:00","2011-04-04T00:00:00","2011-04-05T00:00:00","2011-04-06T00:00:00","2011-04-07T00:00:00","2011-04-08T00:00:00","2011-04-11T00:00:00","2011-04-12T00:00:00","2011-04-13T00:00:00","2011-04-14T00:00:00","2011-04-15T00:00:00","2011-04-18T00:00:00","2011-04-19T00:00:00","2011-04-20T00:00:00","2011-04-21T00:00:00","2011-04-25T00:00:00","2011-04-26T00:00:00","2011-04-27T00:00:00","2011-04-28T00:00:00","2011-04-29T00:00:00","2011-05-02T00:00:00","2011-05-03T00:00:00","2011-05-04T00:00:00","2011-05-05T00:00:00","2011-05-06T00:00:00","2011-05-09T00:00:00","2011-05-10T00:00:00","2011-05-11T00:00:00","2011-05-12T00:00:00","2011-05-13T00:00:00","2011-05-16T00:00:00","2011-05-17T00:00:00","2011-05-18T00:00:00","2011-05-19T00:00:00","2011-05-20T00:00:00","2011-05-23T00:00:00","2011-05-24T00:00:00","2011-05-25T00:00:00","2011-05-26T00:00:00","2011-05-27T00:00:00","2011-05-31T00:00:00","2011-06-01T00:00:00","2011-06-02T00:00:00","2011-06-03T00:00:00","2011-06-06T00:00:00","2011-06-07T00:00:00","2011-06-08T00:00:00","2011-06-09T00:00:00","2011-06-10T00:00:00","2011-06-13T00:00:00","2011-06-14T00:00:00","2011-06-15T00:00:00","2011-06-16T00:00:00","2011-06-17T00:00:00","2011-06-20T00:00:00","2011-06-21T00:00:00","2011-06-22T00:00:00","2011-06-23T00:00:00","2011-06-24T00:00:00","2011-06-27T00:00:00","2011-06-28T00:00:00","2011-06-29T00:00:00","2011-06-30T00:00:00","2011-07-01T00:00:00","2011-07-05T00:00:00","2011-07-06T00:00:00","2011-07-07T00:00:00","2011-07-08T00:00:00","2011-07-11T00:00:00","2011-07-12T00:00:00","2011-07-13T00:00:00","2011-07-14T00:00:00","2011-07-15T00:00:00","2011-07-18T00:00:00","2011-07-19T00:00:00","2011-07-20T00:00:00","2011-07-21T00:00:00","2011-07-22T00:00:00","2011-07-25T00:00:00","2011-07-26T00:00:00","2011-07-27T00:00:00","2011-07-28T00:00:00","2011-07-29T00:00:00","2011-08-01T00:00:00","2011-08-02T00:00:00","2011-08-03T00:00:00","2011-08-04T00:00:00","2011-08-05T00:00:00","2011-08-08T00:00:00","2011-08-09T00:00:00","2011-08-10T00:00:00","2011-08-11T00:00:00","2011-08-12T00:00:00","2011-08-15T00:00:00","2011-08-16T00:00:00","2011-08-17T00:00:00","2011-08-18T00:00:00","2011-08-19T00:00:00","2011-08-22T00:00:00","2011-08-23T00:00:00","2011-08-24T00:00:00","2011-08-25T00:00:00","2011-08-26T00:00:00","2011-08-29T00:00:00","2011-08-30T00:00:00","2011-08-31T00:00:00","2011-09-01T00:00:00","2011-09-02T00:00:00","2011-09-06T00:00:00","2011-09-07T00:00:00","2011-09-08T00:00:00","2011-09-09T00:00:00","2011-09-12T00:00:00","2011-09-13T00:00:00","2011-09-14T00:00:00","2011-09-15T00:00:00","2011-09-16T00:00:00","2011-09-19T00:00:00","2011-09-20T00:00:00","2011-09-21T00:00:00","2011-09-22T00:00:00","2011-09-23T00:00:00","2011-09-26T00:00:00","2011-09-27T00:00:00","2011-09-28T00:00:00","2011-09-29T00:00:00","2011-09-30T00:00:00","2011-10-03T00:00:00","2011-10-04T00:00:00","2011-10-05T00:00:00","2011-10-06T00:00:00","2011-10-07T00:00:00","2011-10-10T00:00:00","2011-10-11T00:00:00","2011-10-12T00:00:00","2011-10-13T00:00:00","2011-10-14T00:00:00","2011-10-17T00:00:00","2011-10-18T00:00:00","2011-10-19T00:00:00","2011-10-20T00:00:00","2011-10-21T00:00:00","2011-10-24T00:00:00","2011-10-25T00:00:00","2011-10-26T00:00:00","2011-10-27T00:00:00","2011-10-28T00:00:00","2011-10-31T00:00:00","2011-11-01T00:00:00","2011-11-02T00:00:00","2011-11-03T00:00:00","2011-11-04T00:00:00","2011-11-07T00:00:00","2011-11-08T00:00:00","2011-11-09T00:00:00","2011-11-10T00:00:00","2011-11-11T00:00:00","2011-11-14T00:00:00","2011-11-15T00:00:00","2011-11-16T00:00:00","2011-11-17T00:00:00","2011-11-18T00:00:00","2011-11-21T00:00:00","2011-11-22T00:00:00","2011-11-23T00:00:00","2011-11-25T00:00:00","2011-11-28T00:00:00","2011-11-29T00:00:00","2011-11-30T00:00:00","2011-12-01T00:00:00","2011-12-02T00:00:00","2011-12-05T00:00:00","2011-12-06T00:00:00","2011-12-07T00:00:00","2011-12-08T00:00:00","2011-12-09T00:00:00","2011-12-12T00:00:00","2011-12-13T00:00:00","2011-12-14T00:00:00","2011-12-15T00:00:00","2011-12-16T00:00:00","2011-12-19T00:00:00","2011-12-20T00:00:00","2011-12-21T00:00:00","2011-12-22T00:00:00","2011-12-23T00:00:00","2011-12-27T00:00:00","2011-12-28T00:00:00","2011-12-29T00:00:00","2011-12-30T00:00:00","2012-01-03T00:00:00","2012-01-04T00:00:00","2012-01-05T00:00:00","2012-01-06T00:00:00","2012-01-09T00:00:00","2012-01-10T00:00:00","2012-01-11T00:00:00","2012-01-12T00:00:00","2012-01-13T00:00:00","2012-01-17T00:00:00","2012-01-18T00:00:00","2012-01-19T00:00:00","2012-01-20T00:00:00","2012-01-23T00:00:00","2012-01-24T00:00:00","2012-01-25T00:00:00","2012-01-26T00:00:00","2012-01-27T00:00:00","2012-01-30T00:00:00","2012-01-31T00:00:00","2012-02-01T00:00:00","2012-02-02T00:00:00","2012-02-03T00:00:00","2012-02-06T00:00:00","2012-02-07T00:00:00","2012-02-08T00:00:00","2012-02-09T00:00:00","2012-02-10T00:00:00","2012-02-13T00:00:00","2012-02-14T00:00:00","2012-02-15T00:00:00","2012-02-16T00:00:00","2012-02-17T00:00:00","2012-02-21T00:00:00","2012-02-22T00:00:00","2012-02-23T00:00:00","2012-02-24T00:00:00","2012-02-27T00:00:00","2012-02-28T00:00:00","2012-02-29T00:00:00","2012-03-01T00:00:00","2012-03-02T00:00:00","2012-03-05T00:00:00","2012-03-06T00:00:00","2012-03-07T00:00:00","2012-03-08T00:00:00","2012-03-09T00:00:00","2012-03-12T00:00:00","2012-03-13T00:00:00","2012-03-14T00:00:00","2012-03-15T00:00:00","2012-03-16T00:00:00","2012-03-19T00:00:00","2012-03-20T00:00:00","2012-03-21T00:00:00","2012-03-22T00:00:00","2012-03-23T00:00:00","2012-03-26T00:00:00","2012-03-27T00:00:00","2012-03-28T00:00:00","2012-03-29T00:00:00","2012-03-30T00:00:00","2012-04-02T00:00:00","2012-04-03T00:00:00","2012-04-04T00:00:00","2012-04-05T00:00:00","2012-04-09T00:00:00","2012-04-10T00:00:00","2012-04-11T00:00:00","2012-04-12T00:00:00","2012-04-13T00:00:00","2012-04-16T00:00:00","2012-04-17T00:00:00","2012-04-18T00:00:00","2012-04-19T00:00:00","2012-04-20T00:00:00","2012-04-23T00:00:00","2012-04-24T00:00:00","2012-04-25T00:00:00","2012-04-26T00:00:00","2012-04-27T00:00:00","2012-04-30T00:00:00","2012-05-01T00:00:00","2012-05-02T00:00:00","2012-05-03T00:00:00","2012-05-04T00:00:00","2012-05-07T00:00:00","2012-05-08T00:00:00","2012-05-09T00:00:00","2012-05-10T00:00:00","2012-05-11T00:00:00","2012-05-14T00:00:00","2012-05-15T00:00:00","2012-05-16T00:00:00","2012-05-17T00:00:00","2012-05-18T00:00:00","2012-05-21T00:00:00","2012-05-22T00:00:00","2012-05-23T00:00:00","2012-05-24T00:00:00","2012-05-25T00:00:00","2012-05-29T00:00:00","2012-05-30T00:00:00","2012-05-31T00:00:00","2012-06-01T00:00:00","2012-06-04T00:00:00","2012-06-05T00:00:00","2012-06-06T00:00:00","2012-06-07T00:00:00","2012-06-08T00:00:00","2012-06-11T00:00:00","2012-06-12T00:00:00","2012-06-13T00:00:00","2012-06-14T00:00:00","2012-06-15T00:00:00","2012-06-18T00:00:00","2012-06-19T00:00:00","2012-06-20T00:00:00","2012-06-21T00:00:00","2012-06-22T00:00:00","2012-06-25T00:00:00","2012-06-26T00:00:00","2012-06-27T00:00:00","2012-06-28T00:00:00","2012-06-29T00:00:00","2012-07-02T00:00:00","2012-07-03T00:00:00","2012-07-05T00:00:00","2012-07-06T00:00:00","2012-07-09T00:00:00","2012-07-10T00:00:00","2012-07-11T00:00:00","2012-07-12T00:00:00","2012-07-13T00:00:00","2012-07-16T00:00:00","2012-07-17T00:00:00","2012-07-18T00:00:00","2012-07-19T00:00:00","2012-07-20T00:00:00","2012-07-23T00:00:00","2012-07-24T00:00:00","2012-07-25T00:00:00","2012-07-26T00:00:00","2012-07-27T00:00:00","2012-07-30T00:00:00","2012-07-31T00:00:00","2012-08-01T00:00:00","2012-08-02T00:00:00","2012-08-03T00:00:00","2012-08-06T00:00:00","2012-08-07T00:00:00","2012-08-08T00:00:00","2012-08-09T00:00:00","2012-08-10T00:00:00","2012-08-13T00:00:00","2012-08-14T00:00:00","2012-08-15T00:00:00","2012-08-16T00:00:00","2012-08-17T00:00:00","2012-08-20T00:00:00","2012-08-21T00:00:00","2012-08-22T00:00:00","2012-08-23T00:00:00","2012-08-24T00:00:00","2012-08-27T00:00:00","2012-08-28T00:00:00","2012-08-29T00:00:00","2012-08-30T00:00:00","2012-08-31T00:00:00","2012-09-04T00:00:00","2012-09-05T00:00:00","2012-09-06T00:00:00","2012-09-07T00:00:00","2012-09-10T00:00:00","2012-09-11T00:00:00","2012-09-12T00:00:00","2012-09-13T00:00:00","2012-09-14T00:00:00","2012-09-17T00:00:00","2012-09-18T00:00:00","2012-09-19T00:00:00","2012-09-20T00:00:00","2012-09-21T00:00:00","2012-09-24T00:00:00","2012-09-25T00:00:00","2012-09-26T00:00:00","2012-09-27T00:00:00","2012-09-28T00:00:00","2012-10-01T00:00:00","2012-10-02T00:00:00","2012-10-03T00:00:00","2012-10-04T00:00:00","2012-10-05T00:00:00","2012-10-08T00:00:00","2012-10-09T00:00:00","2012-10-10T00:00:00","2012-10-11T00:00:00","2012-10-12T00:00:00","2012-10-15T00:00:00","2012-10-16T00:00:00","2012-10-17T00:00:00","2012-10-18T00:00:00","2012-10-19T00:00:00","2012-10-22T00:00:00","2012-10-23T00:00:00","2012-10-24T00:00:00","2012-10-25T00:00:00","2012-10-26T00:00:00","2012-10-31T00:00:00","2012-11-01T00:00:00","2012-11-02T00:00:00","2012-11-05T00:00:00","2012-11-06T00:00:00","2012-11-07T00:00:00","2012-11-08T00:00:00","2012-11-09T00:00:00","2012-11-12T00:00:00","2012-11-13T00:00:00","2012-11-14T00:00:00","2012-11-15T00:00:00","2012-11-16T00:00:00","2012-11-19T00:00:00","2012-11-20T00:00:00","2012-11-21T00:00:00","2012-11-23T00:00:00","2012-11-26T00:00:00","2012-11-27T00:00:00","2012-11-28T00:00:00","2012-11-29T00:00:00","2012-11-30T00:00:00","2012-12-03T00:00:00","2012-12-04T00:00:00","2012-12-05T00:00:00","2012-12-06T00:00:00","2012-12-07T00:00:00","2012-12-10T00:00:00","2012-12-11T00:00:00","2012-12-12T00:00:00","2012-12-13T00:00:00","2012-12-14T00:00:00","2012-12-17T00:00:00","2012-12-18T00:00:00","2012-12-19T00:00:00","2012-12-20T00:00:00","2012-12-21T00:00:00","2012-12-24T00:00:00","2012-12-26T00:00:00","2012-12-27T00:00:00","2012-12-28T00:00:00","2012-12-31T00:00:00","2013-01-02T00:00:00","2013-01-03T00:00:00","2013-01-04T00:00:00","2013-01-07T00:00:00","2013-01-08T00:00:00","2013-01-09T00:00:00","2013-01-10T00:00:00","2013-01-11T00:00:00","2013-01-14T00:00:00","2013-01-15T00:00:00","2013-01-16T00:00:00","2013-01-17T00:00:00","2013-01-18T00:00:00","2013-01-22T00:00:00","2013-01-23T00:00:00","2013-01-24T00:00:00","2013-01-25T00:00:00","2013-01-28T00:00:00","2013-01-29T00:00:00","2013-01-30T00:00:00","2013-01-31T00:00:00","2013-02-01T00:00:00","2013-02-04T00:00:00","2013-02-05T00:00:00","2013-02-06T00:00:00","2013-02-07T00:00:00","2013-02-08T00:00:00","2013-02-11T00:00:00","2013-02-12T00:00:00","2013-02-13T00:00:00","2013-02-14T00:00:00","2013-02-15T00:00:00","2013-02-19T00:00:00","2013-02-20T00:00:00","2013-02-21T00:00:00","2013-02-22T00:00:00","2013-02-25T00:00:00","2013-02-26T00:00:00","2013-02-27T00:00:00","2013-02-28T00:00:00","2013-03-01T00:00:00","2013-03-04T00:00:00","2013-03-05T00:00:00","2013-03-06T00:00:00","2013-03-07T00:00:00","2013-03-08T00:00:00","2013-03-11T00:00:00","2013-03-12T00:00:00","2013-03-13T00:00:00","2013-03-14T00:00:00","2013-03-15T00:00:00","2013-03-18T00:00:00","2013-03-19T00:00:00","2013-03-20T00:00:00","2013-03-21T00:00:00","2013-03-22T00:00:00","2013-03-25T00:00:00","2013-03-26T00:00:00","2013-03-27T00:00:00","2013-03-28T00:00:00","2013-04-01T00:00:00","2013-04-02T00:00:00","2013-04-03T00:00:00","2013-04-04T00:00:00","2013-04-05T00:00:00","2013-04-08T00:00:00","2013-04-09T00:00:00","2013-04-10T00:00:00","2013-04-11T00:00:00","2013-04-12T00:00:00","2013-04-15T00:00:00","2013-04-16T00:00:00","2013-04-17T00:00:00","2013-04-18T00:00:00","2013-04-19T00:00:00","2013-04-22T00:00:00","2013-04-23T00:00:00","2013-04-24T00:00:00","2013-04-25T00:00:00","2013-04-26T00:00:00","2013-04-29T00:00:00","2013-04-30T00:00:00","2013-05-01T00:00:00","2013-05-02T00:00:00","2013-05-03T00:00:00","2013-05-06T00:00:00","2013-05-07T00:00:00","2013-05-08T00:00:00","2013-05-09T00:00:00","2013-05-10T00:00:00","2013-05-13T00:00:00","2013-05-14T00:00:00","2013-05-15T00:00:00","2013-05-16T00:00:00","2013-05-17T00:00:00","2013-05-20T00:00:00","2013-05-21T00:00:00","2013-05-22T00:00:00","2013-05-23T00:00:00","2013-05-24T00:00:00","2013-05-28T00:00:00","2013-05-29T00:00:00","2013-05-30T00:00:00","2013-05-31T00:00:00","2013-06-03T00:00:00","2013-06-04T00:00:00","2013-06-05T00:00:00","2013-06-06T00:00:00","2013-06-07T00:00:00","2013-06-10T00:00:00","2013-06-11T00:00:00","2013-06-12T00:00:00","2013-06-13T00:00:00","2013-06-14T00:00:00","2013-06-17T00:00:00","2013-06-18T00:00:00","2013-06-19T00:00:00","2013-06-20T00:00:00","2013-06-21T00:00:00","2013-06-24T00:00:00","2013-06-25T00:00:00","2013-06-26T00:00:00","2013-06-27T00:00:00","2013-06-28T00:00:00","2013-07-01T00:00:00","2013-07-02T00:00:00","2013-07-03T00:00:00","2013-07-05T00:00:00","2013-07-08T00:00:00","2013-07-09T00:00:00","2013-07-10T00:00:00","2013-07-11T00:00:00","2013-07-12T00:00:00","2013-07-15T00:00:00","2013-07-16T00:00:00","2013-07-17T00:00:00","2013-07-18T00:00:00","2013-07-19T00:00:00","2013-07-22T00:00:00","2013-07-23T00:00:00","2013-07-24T00:00:00","2013-07-25T00:00:00","2013-07-26T00:00:00","2013-07-29T00:00:00","2013-07-30T00:00:00","2013-07-31T00:00:00","2013-08-01T00:00:00","2013-08-02T00:00:00","2013-08-05T00:00:00","2013-08-06T00:00:00","2013-08-07T00:00:00","2013-08-08T00:00:00","2013-08-09T00:00:00","2013-08-12T00:00:00","2013-08-13T00:00:00","2013-08-14T00:00:00","2013-08-15T00:00:00","2013-08-16T00:00:00","2013-08-19T00:00:00","2013-08-20T00:00:00","2013-08-21T00:00:00","2013-08-22T00:00:00","2013-08-23T00:00:00","2013-08-26T00:00:00","2013-08-27T00:00:00","2013-08-28T00:00:00","2013-08-29T00:00:00","2013-08-30T00:00:00","2013-09-03T00:00:00","2013-09-04T00:00:00","2013-09-05T00:00:00","2013-09-06T00:00:00","2013-09-09T00:00:00","2013-09-10T00:00:00","2013-09-11T00:00:00","2013-09-12T00:00:00","2013-09-13T00:00:00","2013-09-16T00:00:00","2013-09-17T00:00:00","2013-09-18T00:00:00","2013-09-19T00:00:00","2013-09-20T00:00:00","2013-09-23T00:00:00","2013-09-24T00:00:00","2013-09-25T00:00:00","2013-09-26T00:00:00","2013-09-27T00:00:00","2013-09-30T00:00:00","2013-10-01T00:00:00","2013-10-02T00:00:00","2013-10-03T00:00:00","2013-10-04T00:00:00","2013-10-07T00:00:00","2013-10-08T00:00:00","2013-10-09T00:00:00","2013-10-10T00:00:00","2013-10-11T00:00:00","2013-10-14T00:00:00","2013-10-15T00:00:00","2013-10-16T00:00:00","2013-10-17T00:00:00","2013-10-18T00:00:00","2013-10-21T00:00:00","2013-10-22T00:00:00","2013-10-23T00:00:00","2013-10-24T00:00:00","2013-10-25T00:00:00","2013-10-28T00:00:00","2013-10-29T00:00:00","2013-10-30T00:00:00","2013-10-31T00:00:00","2013-11-01T00:00:00","2013-11-04T00:00:00","2013-11-05T00:00:00","2013-11-06T00:00:00","2013-11-07T00:00:00","2013-11-08T00:00:00","2013-11-11T00:00:00","2013-11-12T00:00:00","2013-11-13T00:00:00","2013-11-14T00:00:00","2013-11-15T00:00:00","2013-11-18T00:00:00","2013-11-19T00:00:00","2013-11-20T00:00:00","2013-11-21T00:00:00","2013-11-22T00:00:00","2013-11-25T00:00:00","2013-11-26T00:00:00","2013-11-27T00:00:00","2013-11-29T00:00:00","2013-12-02T00:00:00","2013-12-03T00:00:00","2013-12-04T00:00:00","2013-12-05T00:00:00","2013-12-06T00:00:00","2013-12-09T00:00:00","2013-12-10T00:00:00","2013-12-11T00:00:00","2013-12-12T00:00:00","2013-12-13T00:00:00","2013-12-16T00:00:00","2013-12-17T00:00:00","2013-12-18T00:00:00","2013-12-19T00:00:00","2013-12-20T00:00:00","2013-12-23T00:00:00","2013-12-24T00:00:00","2013-12-26T00:00:00","2013-12-27T00:00:00","2013-12-30T00:00:00","2013-12-31T00:00:00","2014-01-02T00:00:00","2014-01-03T00:00:00","2014-01-06T00:00:00","2014-01-07T00:00:00","2014-01-08T00:00:00","2014-01-09T00:00:00","2014-01-10T00:00:00","2014-01-13T00:00:00","2014-01-14T00:00:00","2014-01-15T00:00:00","2014-01-16T00:00:00","2014-01-17T00:00:00","2014-01-21T00:00:00","2014-01-22T00:00:00","2014-01-23T00:00:00","2014-01-24T00:00:00","2014-01-27T00:00:00","2014-01-28T00:00:00","2014-01-29T00:00:00","2014-01-30T00:00:00","2014-01-31T00:00:00","2014-02-03T00:00:00","2014-02-04T00:00:00","2014-02-05T00:00:00","2014-02-06T00:00:00","2014-02-07T00:00:00","2014-02-10T00:00:00","2014-02-11T00:00:00","2014-02-12T00:00:00","2014-02-13T00:00:00","2014-02-14T00:00:00","2014-02-18T00:00:00","2014-02-19T00:00:00","2014-02-20T00:00:00","2014-02-21T00:00:00","2014-02-24T00:00:00","2014-02-25T00:00:00","2014-02-26T00:00:00","2014-02-27T00:00:00","2014-02-28T00:00:00","2014-03-03T00:00:00","2014-03-04T00:00:00","2014-03-05T00:00:00","2014-03-06T00:00:00","2014-03-07T00:00:00","2014-03-10T00:00:00","2014-03-11T00:00:00","2014-03-12T00:00:00","2014-03-13T00:00:00","2014-03-14T00:00:00","2014-03-17T00:00:00","2014-03-18T00:00:00","2014-03-19T00:00:00","2014-03-20T00:00:00","2014-03-21T00:00:00","2014-03-24T00:00:00","2014-03-25T00:00:00","2014-03-26T00:00:00","2014-03-27T00:00:00","2014-03-28T00:00:00","2014-03-31T00:00:00","2014-04-01T00:00:00","2014-04-02T00:00:00","2014-04-03T00:00:00","2014-04-04T00:00:00","2014-04-07T00:00:00","2014-04-08T00:00:00","2014-04-09T00:00:00","2014-04-10T00:00:00","2014-04-11T00:00:00","2014-04-14T00:00:00","2014-04-15T00:00:00","2014-04-16T00:00:00","2014-04-17T00:00:00","2014-04-21T00:00:00","2014-04-22T00:00:00","2014-04-23T00:00:00","2014-04-24T00:00:00","2014-04-25T00:00:00","2014-04-28T00:00:00","2014-04-29T00:00:00","2014-04-30T00:00:00","2014-05-01T00:00:00","2014-05-02T00:00:00","2014-05-05T00:00:00","2014-05-06T00:00:00","2014-05-07T00:00:00","2014-05-08T00:00:00","2014-05-09T00:00:00","2014-05-12T00:00:00","2014-05-13T00:00:00","2014-05-14T00:00:00","2014-05-15T00:00:00","2014-05-16T00:00:00","2014-05-19T00:00:00","2014-05-20T00:00:00","2014-05-21T00:00:00","2014-05-22T00:00:00","2014-05-23T00:00:00","2014-05-27T00:00:00","2014-05-28T00:00:00","2014-05-29T00:00:00","2014-05-30T00:00:00","2014-06-02T00:00:00","2014-06-03T00:00:00","2014-06-04T00:00:00","2014-06-05T00:00:00","2014-06-06T00:00:00","2014-06-09T00:00:00","2014-06-10T00:00:00","2014-06-11T00:00:00","2014-06-12T00:00:00","2014-06-13T00:00:00","2014-06-16T00:00:00","2014-06-17T00:00:00","2014-06-18T00:00:00","2014-06-19T00:00:00","2014-06-20T00:00:00","2014-06-23T00:00:00","2014-06-24T00:00:00","2014-06-25T00:00:00","2014-06-26T00:00:00","2014-06-27T00:00:00","2014-06-30T00:00:00","2014-07-01T00:00:00","2014-07-02T00:00:00","2014-07-03T00:00:00","2014-07-07T00:00:00","2014-07-08T00:00:00","2014-07-09T00:00:00","2014-07-10T00:00:00","2014-07-11T00:00:00","2014-07-14T00:00:00","2014-07-15T00:00:00","2014-07-16T00:00:00","2014-07-17T00:00:00","2014-07-18T00:00:00","2014-07-21T00:00:00","2014-07-22T00:00:00","2014-07-23T00:00:00","2014-07-24T00:00:00","2014-07-25T00:00:00","2014-07-28T00:00:00","2014-07-29T00:00:00","2014-07-30T00:00:00","2014-07-31T00:00:00","2014-08-01T00:00:00","2014-08-04T00:00:00","2014-08-05T00:00:00","2014-08-06T00:00:00","2014-08-07T00:00:00","2014-08-08T00:00:00","2014-08-11T00:00:00","2014-08-12T00:00:00","2014-08-13T00:00:00","2014-08-14T00:00:00","2014-08-15T00:00:00","2014-08-18T00:00:00","2014-08-19T00:00:00","2014-08-20T00:00:00","2014-08-21T00:00:00","2014-08-22T00:00:00","2014-08-25T00:00:00","2014-08-26T00:00:00","2014-08-27T00:00:00","2014-08-28T00:00:00","2014-08-29T00:00:00","2014-09-02T00:00:00","2014-09-03T00:00:00","2014-09-04T00:00:00","2014-09-05T00:00:00","2014-09-08T00:00:00","2014-09-09T00:00:00","2014-09-10T00:00:00","2014-09-11T00:00:00","2014-09-12T00:00:00","2014-09-15T00:00:00","2014-09-16T00:00:00","2014-09-17T00:00:00","2014-09-18T00:00:00","2014-09-19T00:00:00","2014-09-22T00:00:00","2014-09-23T00:00:00","2014-09-24T00:00:00","2014-09-25T00:00:00","2014-09-26T00:00:00","2014-09-29T00:00:00","2014-09-30T00:00:00","2014-10-01T00:00:00","2014-10-02T00:00:00","2014-10-03T00:00:00","2014-10-06T00:00:00","2014-10-07T00:00:00","2014-10-08T00:00:00","2014-10-09T00:00:00","2014-10-10T00:00:00","2014-10-13T00:00:00","2014-10-14T00:00:00","2014-10-15T00:00:00","2014-10-16T00:00:00","2014-10-17T00:00:00","2014-10-20T00:00:00","2014-10-21T00:00:00","2014-10-22T00:00:00","2014-10-23T00:00:00","2014-10-24T00:00:00","2014-10-27T00:00:00","2014-10-28T00:00:00","2014-10-29T00:00:00","2014-10-30T00:00:00","2014-10-31T00:00:00","2014-11-03T00:00:00","2014-11-04T00:00:00","2014-11-05T00:00:00","2014-11-06T00:00:00","2014-11-07T00:00:00","2014-11-10T00:00:00","2014-11-11T00:00:00","2014-11-12T00:00:00","2014-11-13T00:00:00","2014-11-14T00:00:00","2014-11-17T00:00:00","2014-11-18T00:00:00","2014-11-19T00:00:00","2014-11-20T00:00:00","2014-11-21T00:00:00","2014-11-24T00:00:00","2014-11-25T00:00:00","2014-11-26T00:00:00","2014-11-28T00:00:00","2014-12-01T00:00:00","2014-12-02T00:00:00","2014-12-03T00:00:00","2014-12-04T00:00:00","2014-12-05T00:00:00","2014-12-08T00:00:00","2014-12-09T00:00:00","2014-12-10T00:00:00","2014-12-11T00:00:00","2014-12-12T00:00:00","2014-12-15T00:00:00","2014-12-16T00:00:00","2014-12-17T00:00:00","2014-12-18T00:00:00","2014-12-19T00:00:00","2014-12-22T00:00:00","2014-12-23T00:00:00","2014-12-24T00:00:00","2014-12-26T00:00:00","2014-12-29T00:00:00","2014-12-30T00:00:00","2014-12-31T00:00:00","2015-01-02T00:00:00","2015-01-05T00:00:00","2015-01-06T00:00:00","2015-01-07T00:00:00","2015-01-08T00:00:00","2015-01-09T00:00:00","2015-01-12T00:00:00","2015-01-13T00:00:00","2015-01-14T00:00:00","2015-01-15T00:00:00","2015-01-16T00:00:00","2015-01-20T00:00:00","2015-01-21T00:00:00","2015-01-22T00:00:00","2015-01-23T00:00:00","2015-01-26T00:00:00","2015-01-27T00:00:00","2015-01-28T00:00:00","2015-01-29T00:00:00","2015-01-30T00:00:00","2015-02-02T00:00:00","2015-02-03T00:00:00","2015-02-04T00:00:00","2015-02-05T00:00:00","2015-02-06T00:00:00","2015-02-09T00:00:00","2015-02-10T00:00:00","2015-02-11T00:00:00","2015-02-12T00:00:00","2015-02-13T00:00:00","2015-02-17T00:00:00","2015-02-18T00:00:00","2015-02-19T00:00:00","2015-02-20T00:00:00","2015-02-23T00:00:00","2015-02-24T00:00:00","2015-02-25T00:00:00","2015-02-26T00:00:00","2015-02-27T00:00:00","2015-03-02T00:00:00","2015-03-03T00:00:00","2015-03-04T00:00:00","2015-03-05T00:00:00","2015-03-06T00:00:00","2015-03-09T00:00:00","2015-03-10T00:00:00","2015-03-11T00:00:00","2015-03-12T00:00:00","2015-03-13T00:00:00","2015-03-16T00:00:00","2015-03-17T00:00:00","2015-03-18T00:00:00","2015-03-19T00:00:00","2015-03-20T00:00:00","2015-03-23T00:00:00","2015-03-24T00:00:00","2015-03-25T00:00:00","2015-03-26T00:00:00","2015-03-27T00:00:00","2015-03-30T00:00:00","2015-03-31T00:00:00","2015-04-01T00:00:00","2015-04-02T00:00:00","2015-04-06T00:00:00","2015-04-07T00:00:00","2015-04-08T00:00:00","2015-04-09T00:00:00","2015-04-10T00:00:00","2015-04-13T00:00:00","2015-04-14T00:00:00","2015-04-15T00:00:00","2015-04-16T00:00:00","2015-04-17T00:00:00","2015-04-20T00:00:00","2015-04-21T00:00:00","2015-04-22T00:00:00","2015-04-23T00:00:00","2015-04-24T00:00:00","2015-04-27T00:00:00","2015-04-28T00:00:00","2015-04-29T00:00:00","2015-04-30T00:00:00","2015-05-01T00:00:00","2015-05-04T00:00:00","2015-05-05T00:00:00","2015-05-06T00:00:00","2015-05-07T00:00:00","2015-05-08T00:00:00","2015-05-11T00:00:00","2015-05-12T00:00:00","2015-05-13T00:00:00","2015-05-14T00:00:00","2015-05-15T00:00:00","2015-05-18T00:00:00","2015-05-19T00:00:00","2015-05-20T00:00:00","2015-05-21T00:00:00","2015-05-22T00:00:00","2015-05-26T00:00:00","2015-05-27T00:00:00","2015-05-28T00:00:00","2015-05-29T00:00:00","2015-06-01T00:00:00","2015-06-02T00:00:00","2015-06-03T00:00:00","2015-06-04T00:00:00","2015-06-05T00:00:00","2015-06-08T00:00:00","2015-06-09T00:00:00","2015-06-10T00:00:00","2015-06-11T00:00:00","2015-06-12T00:00:00","2015-06-15T00:00:00","2015-06-16T00:00:00","2015-06-17T00:00:00","2015-06-18T00:00:00","2015-06-19T00:00:00","2015-06-22T00:00:00","2015-06-23T00:00:00","2015-06-24T00:00:00","2015-06-25T00:00:00","2015-06-26T00:00:00","2015-06-29T00:00:00","2015-06-30T00:00:00","2015-07-01T00:00:00","2015-07-02T00:00:00","2015-07-06T00:00:00","2015-07-07T00:00:00","2015-07-08T00:00:00","2015-07-09T00:00:00","2015-07-10T00:00:00","2015-07-13T00:00:00","2015-07-14T00:00:00","2015-07-15T00:00:00","2015-07-16T00:00:00","2015-07-17T00:00:00","2015-07-20T00:00:00","2015-07-21T00:00:00","2015-07-22T00:00:00","2015-07-23T00:00:00","2015-07-24T00:00:00","2015-07-27T00:00:00","2015-07-28T00:00:00","2015-07-29T00:00:00","2015-07-30T00:00:00","2015-07-31T00:00:00","2015-08-03T00:00:00","2015-08-04T00:00:00","2015-08-05T00:00:00","2015-08-06T00:00:00","2015-08-07T00:00:00","2015-08-10T00:00:00","2015-08-11T00:00:00","2015-08-12T00:00:00","2015-08-13T00:00:00","2015-08-14T00:00:00","2015-08-17T00:00:00","2015-08-18T00:00:00","2015-08-19T00:00:00","2015-08-20T00:00:00","2015-08-21T00:00:00","2015-08-24T00:00:00","2015-08-25T00:00:00","2015-08-26T00:00:00","2015-08-27T00:00:00","2015-08-28T00:00:00","2015-08-31T00:00:00","2015-09-01T00:00:00","2015-09-02T00:00:00","2015-09-03T00:00:00","2015-09-04T00:00:00","2015-09-08T00:00:00","2015-09-09T00:00:00","2015-09-10T00:00:00","2015-09-11T00:00:00","2015-09-14T00:00:00","2015-09-15T00:00:00","2015-09-16T00:00:00","2015-09-17T00:00:00","2015-09-18T00:00:00","2015-09-21T00:00:00","2015-09-22T00:00:00","2015-09-23T00:00:00","2015-09-24T00:00:00","2015-09-25T00:00:00","2015-09-28T00:00:00","2015-09-29T00:00:00","2015-09-30T00:00:00","2015-10-01T00:00:00","2015-10-02T00:00:00","2015-10-05T00:00:00","2015-10-06T00:00:00","2015-10-07T00:00:00","2015-10-08T00:00:00","2015-10-09T00:00:00","2015-10-12T00:00:00","2015-10-13T00:00:00","2015-10-14T00:00:00","2015-10-15T00:00:00","2015-10-16T00:00:00","2015-10-19T00:00:00","2015-10-20T00:00:00","2015-10-21T00:00:00","2015-10-22T00:00:00","2015-10-23T00:00:00","2015-10-26T00:00:00","2015-10-27T00:00:00","2015-10-28T00:00:00","2015-10-29T00:00:00","2015-10-30T00:00:00","2015-11-02T00:00:00","2015-11-03T00:00:00","2015-11-04T00:00:00","2015-11-05T00:00:00","2015-11-06T00:00:00","2015-11-09T00:00:00","2015-11-10T00:00:00","2015-11-11T00:00:00","2015-11-12T00:00:00","2015-11-13T00:00:00","2015-11-16T00:00:00","2015-11-17T00:00:00","2015-11-18T00:00:00","2015-11-19T00:00:00","2015-11-20T00:00:00","2015-11-23T00:00:00","2015-11-24T00:00:00","2015-11-25T00:00:00","2015-11-27T00:00:00","2015-11-30T00:00:00","2015-12-01T00:00:00","2015-12-02T00:00:00","2015-12-03T00:00:00","2015-12-04T00:00:00","2015-12-07T00:00:00","2015-12-08T00:00:00","2015-12-09T00:00:00","2015-12-10T00:00:00","2015-12-11T00:00:00","2015-12-14T00:00:00","2015-12-15T00:00:00","2015-12-16T00:00:00","2015-12-17T00:00:00","2015-12-18T00:00:00","2015-12-21T00:00:00","2015-12-22T00:00:00","2015-12-23T00:00:00","2015-12-24T00:00:00","2015-12-28T00:00:00","2015-12-29T00:00:00","2015-12-30T00:00:00","2015-12-31T00:00:00","2016-01-04T00:00:00","2016-01-05T00:00:00","2016-01-06T00:00:00","2016-01-07T00:00:00","2016-01-08T00:00:00","2016-01-11T00:00:00","2016-01-12T00:00:00","2016-01-13T00:00:00","2016-01-14T00:00:00","2016-01-15T00:00:00","2016-01-19T00:00:00","2016-01-20T00:00:00","2016-01-21T00:00:00","2016-01-22T00:00:00","2016-01-25T00:00:00","2016-01-26T00:00:00","2016-01-27T00:00:00","2016-01-28T00:00:00","2016-01-29T00:00:00","2016-02-01T00:00:00","2016-02-02T00:00:00","2016-02-03T00:00:00","2016-02-04T00:00:00","2016-02-05T00:00:00","2016-02-08T00:00:00","2016-02-09T00:00:00","2016-02-10T00:00:00","2016-02-11T00:00:00","2016-02-12T00:00:00","2016-02-16T00:00:00","2016-02-17T00:00:00","2016-02-18T00:00:00","2016-02-19T00:00:00","2016-02-22T00:00:00","2016-02-23T00:00:00","2016-02-24T00:00:00","2016-02-25T00:00:00","2016-02-26T00:00:00","2016-02-29T00:00:00","2016-03-01T00:00:00","2016-03-02T00:00:00","2016-03-03T00:00:00","2016-03-04T00:00:00","2016-03-07T00:00:00","2016-03-08T00:00:00","2016-03-09T00:00:00","2016-03-10T00:00:00","2016-03-11T00:00:00","2016-03-14T00:00:00","2016-03-15T00:00:00","2016-03-16T00:00:00","2016-03-17T00:00:00","2016-03-18T00:00:00","2016-03-21T00:00:00","2016-03-22T00:00:00","2016-03-23T00:00:00","2016-03-24T00:00:00","2016-03-28T00:00:00","2016-03-29T00:00:00","2016-03-30T00:00:00","2016-03-31T00:00:00","2016-04-01T00:00:00","2016-04-04T00:00:00","2016-04-05T00:00:00","2016-04-06T00:00:00","2016-04-07T00:00:00","2016-04-08T00:00:00","2016-04-11T00:00:00","2016-04-12T00:00:00","2016-04-13T00:00:00","2016-04-14T00:00:00","2016-04-15T00:00:00","2016-04-18T00:00:00","2016-04-19T00:00:00","2016-04-20T00:00:00","2016-04-21T00:00:00","2016-04-22T00:00:00","2016-04-25T00:00:00","2016-04-26T00:00:00","2016-04-27T00:00:00","2016-04-28T00:00:00","2016-04-29T00:00:00","2016-05-02T00:00:00","2016-05-03T00:00:00","2016-05-04T00:00:00","2016-05-05T00:00:00","2016-05-06T00:00:00","2016-05-09T00:00:00","2016-05-10T00:00:00","2016-05-11T00:00:00","2016-05-12T00:00:00","2016-05-13T00:00:00","2016-05-16T00:00:00","2016-05-17T00:00:00","2016-05-18T00:00:00","2016-05-19T00:00:00","2016-05-20T00:00:00","2016-05-23T00:00:00","2016-05-24T00:00:00","2016-05-25T00:00:00","2016-05-26T00:00:00","2016-05-27T00:00:00","2016-05-31T00:00:00","2016-06-01T00:00:00","2016-06-02T00:00:00","2016-06-03T00:00:00","2016-06-06T00:00:00","2016-06-07T00:00:00","2016-06-08T00:00:00","2016-06-09T00:00:00","2016-06-10T00:00:00","2016-06-13T00:00:00","2016-06-14T00:00:00","2016-06-15T00:00:00","2016-06-16T00:00:00","2016-06-17T00:00:00","2016-06-20T00:00:00","2016-06-21T00:00:00","2016-06-22T00:00:00","2016-06-23T00:00:00","2016-06-24T00:00:00","2016-06-27T00:00:00","2016-06-28T00:00:00","2016-06-29T00:00:00","2016-06-30T00:00:00","2016-07-01T00:00:00","2016-07-05T00:00:00","2016-07-06T00:00:00","2016-07-07T00:00:00","2016-07-08T00:00:00","2016-07-11T00:00:00","2016-07-12T00:00:00","2016-07-13T00:00:00","2016-07-14T00:00:00","2016-07-15T00:00:00","2016-07-18T00:00:00","2016-07-19T00:00:00","2016-07-20T00:00:00","2016-07-21T00:00:00","2016-07-22T00:00:00","2016-07-25T00:00:00","2016-07-26T00:00:00","2016-07-27T00:00:00","2016-07-28T00:00:00","2016-07-29T00:00:00","2016-08-01T00:00:00","2016-08-02T00:00:00","2016-08-03T00:00:00","2016-08-04T00:00:00","2016-08-05T00:00:00","2016-08-08T00:00:00","2016-08-09T00:00:00","2016-08-10T00:00:00","2016-08-11T00:00:00","2016-08-12T00:00:00","2016-08-15T00:00:00","2016-08-16T00:00:00","2016-08-17T00:00:00","2016-08-18T00:00:00","2016-08-19T00:00:00","2016-08-22T00:00:00","2016-08-23T00:00:00","2016-08-24T00:00:00","2016-08-25T00:00:00","2016-08-26T00:00:00","2016-08-29T00:00:00","2016-08-30T00:00:00","2016-08-31T00:00:00","2016-09-01T00:00:00","2016-09-02T00:00:00","2016-09-06T00:00:00","2016-09-07T00:00:00","2016-09-08T00:00:00","2016-09-09T00:00:00","2016-09-12T00:00:00","2016-09-13T00:00:00","2016-09-14T00:00:00","2016-09-15T00:00:00","2016-09-16T00:00:00","2016-09-19T00:00:00","2016-09-20T00:00:00","2016-09-21T00:00:00","2016-09-22T00:00:00","2016-09-23T00:00:00","2016-09-26T00:00:00","2016-09-27T00:00:00","2016-09-28T00:00:00","2016-09-29T00:00:00","2016-09-30T00:00:00","2016-10-03T00:00:00","2016-10-04T00:00:00","2016-10-05T00:00:00","2016-10-06T00:00:00","2016-10-07T00:00:00","2016-10-10T00:00:00","2016-10-11T00:00:00","2016-10-12T00:00:00","2016-10-13T00:00:00","2016-10-14T00:00:00","2016-10-17T00:00:00","2016-10-18T00:00:00","2016-10-19T00:00:00","2016-10-20T00:00:00","2016-10-21T00:00:00","2016-10-24T00:00:00","2016-10-25T00:00:00","2016-10-26T00:00:00","2016-10-27T00:00:00","2016-10-28T00:00:00","2016-10-31T00:00:00","2016-11-01T00:00:00","2016-11-02T00:00:00","2016-11-03T00:00:00","2016-11-04T00:00:00","2016-11-07T00:00:00","2016-11-08T00:00:00","2016-11-09T00:00:00","2016-11-10T00:00:00","2016-11-11T00:00:00","2016-11-14T00:00:00","2016-11-15T00:00:00","2016-11-16T00:00:00","2016-11-17T00:00:00","2016-11-18T00:00:00","2016-11-21T00:00:00","2016-11-22T00:00:00","2016-11-23T00:00:00","2016-11-25T00:00:00","2016-11-28T00:00:00","2016-11-29T00:00:00","2016-11-30T00:00:00","2016-12-01T00:00:00","2016-12-02T00:00:00","2016-12-05T00:00:00","2016-12-06T00:00:00","2016-12-07T00:00:00","2016-12-08T00:00:00","2016-12-09T00:00:00","2016-12-12T00:00:00","2016-12-13T00:00:00","2016-12-14T00:00:00","2016-12-15T00:00:00","2016-12-16T00:00:00","2016-12-19T00:00:00","2016-12-20T00:00:00","2016-12-21T00:00:00","2016-12-22T00:00:00","2016-12-23T00:00:00","2016-12-27T00:00:00","2016-12-28T00:00:00","2016-12-29T00:00:00","2016-12-30T00:00:00","2017-01-03T00:00:00","2017-01-04T00:00:00","2017-01-05T00:00:00","2017-01-06T00:00:00","2017-01-09T00:00:00","2017-01-10T00:00:00","2017-01-11T00:00:00","2017-01-12T00:00:00","2017-01-13T00:00:00","2017-01-17T00:00:00","2017-01-18T00:00:00","2017-01-19T00:00:00","2017-01-20T00:00:00","2017-01-23T00:00:00","2017-01-24T00:00:00","2017-01-25T00:00:00","2017-01-26T00:00:00","2017-01-27T00:00:00","2017-01-30T00:00:00","2017-01-31T00:00:00","2017-02-01T00:00:00","2017-02-02T00:00:00","2017-02-03T00:00:00","2017-02-06T00:00:00","2017-02-07T00:00:00","2017-02-08T00:00:00","2017-02-09T00:00:00","2017-02-10T00:00:00","2017-02-13T00:00:00","2017-02-14T00:00:00","2017-02-15T00:00:00","2017-02-16T00:00:00","2017-02-17T00:00:00","2017-02-21T00:00:00","2017-02-22T00:00:00","2017-02-23T00:00:00","2017-02-24T00:00:00","2017-02-27T00:00:00","2017-02-28T00:00:00","2017-03-01T00:00:00","2017-03-02T00:00:00","2017-03-03T00:00:00","2017-03-06T00:00:00","2017-03-07T00:00:00","2017-03-08T00:00:00","2017-03-09T00:00:00","2017-03-10T00:00:00","2017-03-13T00:00:00","2017-03-14T00:00:00","2017-03-15T00:00:00","2017-03-16T00:00:00","2017-03-17T00:00:00","2017-03-20T00:00:00","2017-03-21T00:00:00","2017-03-22T00:00:00","2017-03-23T00:00:00","2017-03-24T00:00:00","2017-03-27T00:00:00","2017-03-28T00:00:00","2017-03-29T00:00:00","2017-03-30T00:00:00","2017-03-31T00:00:00","2017-04-03T00:00:00","2017-04-04T00:00:00","2017-04-05T00:00:00","2017-04-06T00:00:00","2017-04-07T00:00:00","2017-04-10T00:00:00","2017-04-11T00:00:00","2017-04-12T00:00:00","2017-04-13T00:00:00","2017-04-17T00:00:00","2017-04-18T00:00:00","2017-04-19T00:00:00","2017-04-20T00:00:00","2017-04-21T00:00:00","2017-04-24T00:00:00","2017-04-25T00:00:00","2017-04-26T00:00:00","2017-04-27T00:00:00","2017-04-28T00:00:00","2017-05-01T00:00:00","2017-05-02T00:00:00","2017-05-03T00:00:00","2017-05-04T00:00:00","2017-05-05T00:00:00","2017-05-08T00:00:00","2017-05-09T00:00:00","2017-05-10T00:00:00","2017-05-11T00:00:00","2017-05-12T00:00:00","2017-05-15T00:00:00","2017-05-16T00:00:00","2017-05-17T00:00:00","2017-05-18T00:00:00","2017-05-19T00:00:00","2017-05-22T00:00:00","2017-05-23T00:00:00","2017-05-24T00:00:00","2017-05-25T00:00:00","2017-05-26T00:00:00","2017-05-30T00:00:00","2017-05-31T00:00:00","2017-06-01T00:00:00","2017-06-02T00:00:00","2017-06-05T00:00:00","2017-06-06T00:00:00","2017-06-07T00:00:00","2017-06-08T00:00:00","2017-06-09T00:00:00","2017-06-12T00:00:00","2017-06-13T00:00:00","2017-06-14T00:00:00","2017-06-15T00:00:00","2017-06-16T00:00:00","2017-06-19T00:00:00","2017-06-20T00:00:00","2017-06-21T00:00:00","2017-06-22T00:00:00","2017-06-23T00:00:00","2017-06-26T00:00:00","2017-06-27T00:00:00","2017-06-28T00:00:00","2017-06-29T00:00:00","2017-06-30T00:00:00","2017-07-03T00:00:00","2017-07-05T00:00:00","2017-07-06T00:00:00","2017-07-07T00:00:00","2017-07-10T00:00:00","2017-07-11T00:00:00","2017-07-12T00:00:00","2017-07-13T00:00:00","2017-07-14T00:00:00","2017-07-17T00:00:00","2017-07-18T00:00:00","2017-07-19T00:00:00","2017-07-20T00:00:00","2017-07-21T00:00:00","2017-07-24T00:00:00","2017-07-25T00:00:00","2017-07-26T00:00:00","2017-07-27T00:00:00","2017-07-28T00:00:00","2017-07-31T00:00:00","2017-08-01T00:00:00","2017-08-02T00:00:00","2017-08-03T00:00:00","2017-08-04T00:00:00","2017-08-07T00:00:00","2017-08-08T00:00:00","2017-08-09T00:00:00","2017-08-10T00:00:00","2017-08-11T00:00:00","2017-08-14T00:00:00","2017-08-15T00:00:00","2017-08-16T00:00:00","2017-08-17T00:00:00","2017-08-18T00:00:00","2017-08-21T00:00:00","2017-08-22T00:00:00","2017-08-23T00:00:00","2017-08-24T00:00:00","2017-08-25T00:00:00","2017-08-28T00:00:00","2017-08-29T00:00:00","2017-08-30T00:00:00","2017-08-31T00:00:00","2017-09-01T00:00:00","2017-09-05T00:00:00","2017-09-06T00:00:00","2017-09-07T00:00:00","2017-09-08T00:00:00","2017-09-11T00:00:00","2017-09-12T00:00:00","2017-09-13T00:00:00","2017-09-14T00:00:00","2017-09-15T00:00:00","2017-09-18T00:00:00","2017-09-19T00:00:00","2017-09-20T00:00:00","2017-09-21T00:00:00","2017-09-22T00:00:00","2017-09-25T00:00:00","2017-09-26T00:00:00","2017-09-27T00:00:00","2017-09-28T00:00:00","2017-09-29T00:00:00","2017-10-02T00:00:00","2017-10-03T00:00:00","2017-10-04T00:00:00","2017-10-05T00:00:00","2017-10-06T00:00:00","2017-10-09T00:00:00","2017-10-10T00:00:00","2017-10-11T00:00:00","2017-10-12T00:00:00","2017-10-13T00:00:00","2017-10-16T00:00:00","2017-10-17T00:00:00","2017-10-18T00:00:00","2017-10-19T00:00:00","2017-10-20T00:00:00","2017-10-23T00:00:00","2017-10-24T00:00:00","2017-10-25T00:00:00","2017-10-26T00:00:00","2017-10-27T00:00:00","2017-10-30T00:00:00","2017-10-31T00:00:00","2017-11-01T00:00:00","2017-11-02T00:00:00","2017-11-03T00:00:00","2017-11-06T00:00:00","2017-11-07T00:00:00","2017-11-08T00:00:00","2017-11-09T00:00:00","2017-11-10T00:00:00","2017-11-13T00:00:00","2017-11-14T00:00:00","2017-11-15T00:00:00","2017-11-16T00:00:00","2017-11-17T00:00:00","2017-11-20T00:00:00","2017-11-21T00:00:00","2017-11-22T00:00:00","2017-11-24T00:00:00","2017-11-27T00:00:00","2017-11-28T00:00:00","2017-11-29T00:00:00","2017-11-30T00:00:00","2017-12-01T00:00:00","2017-12-04T00:00:00","2017-12-05T00:00:00","2017-12-06T00:00:00","2017-12-07T00:00:00","2017-12-08T00:00:00","2017-12-11T00:00:00","2017-12-12T00:00:00","2017-12-13T00:00:00","2017-12-14T00:00:00","2017-12-15T00:00:00","2017-12-18T00:00:00","2017-12-19T00:00:00","2017-12-20T00:00:00","2017-12-21T00:00:00","2017-12-22T00:00:00","2017-12-26T00:00:00","2017-12-27T00:00:00","2017-12-28T00:00:00","2017-12-29T00:00:00","2018-01-02T00:00:00","2018-01-03T00:00:00","2018-01-04T00:00:00","2018-01-05T00:00:00","2018-01-08T00:00:00","2018-01-09T00:00:00","2018-01-10T00:00:00","2018-01-11T00:00:00","2018-01-12T00:00:00","2018-01-16T00:00:00","2018-01-17T00:00:00","2018-01-18T00:00:00","2018-01-19T00:00:00","2018-01-22T00:00:00","2018-01-23T00:00:00","2018-01-24T00:00:00","2018-01-25T00:00:00","2018-01-26T00:00:00","2018-01-29T00:00:00","2018-01-30T00:00:00","2018-01-31T00:00:00","2018-02-01T00:00:00","2018-02-02T00:00:00","2018-02-05T00:00:00","2018-02-06T00:00:00","2018-02-07T00:00:00","2018-02-08T00:00:00","2018-02-09T00:00:00","2018-02-12T00:00:00","2018-02-13T00:00:00","2018-02-14T00:00:00","2018-02-15T00:00:00","2018-02-16T00:00:00","2018-02-20T00:00:00","2018-02-21T00:00:00","2018-02-22T00:00:00","2018-02-23T00:00:00","2018-02-26T00:00:00","2018-02-27T00:00:00","2018-02-28T00:00:00","2018-03-01T00:00:00","2018-03-02T00:00:00","2018-03-05T00:00:00","2018-03-06T00:00:00","2018-03-07T00:00:00","2018-03-08T00:00:00","2018-03-09T00:00:00","2018-03-12T00:00:00","2018-03-13T00:00:00","2018-03-14T00:00:00","2018-03-15T00:00:00","2018-03-16T00:00:00","2018-03-19T00:00:00","2018-03-20T00:00:00","2018-03-21T00:00:00","2018-03-22T00:00:00","2018-03-23T00:00:00","2018-03-26T00:00:00","2018-03-27T00:00:00","2018-03-28T00:00:00","2018-03-29T00:00:00","2018-04-02T00:00:00","2018-04-03T00:00:00","2018-04-04T00:00:00","2018-04-05T00:00:00","2018-04-06T00:00:00","2018-04-09T00:00:00","2018-04-10T00:00:00","2018-04-11T00:00:00","2018-04-12T00:00:00","2018-04-13T00:00:00","2018-04-16T00:00:00","2018-04-17T00:00:00","2018-04-18T00:00:00","2018-04-19T00:00:00","2018-04-20T00:00:00","2018-04-23T00:00:00","2018-04-24T00:00:00","2018-04-25T00:00:00","2018-04-26T00:00:00","2018-04-27T00:00:00","2018-04-30T00:00:00","2018-05-01T00:00:00","2018-05-02T00:00:00","2018-05-03T00:00:00","2018-05-04T00:00:00","2018-05-07T00:00:00","2018-05-08T00:00:00","2018-05-09T00:00:00","2018-05-10T00:00:00","2018-05-11T00:00:00","2018-05-14T00:00:00","2018-05-15T00:00:00","2018-05-16T00:00:00","2018-05-17T00:00:00","2018-05-18T00:00:00","2018-05-21T00:00:00","2018-05-22T00:00:00","2018-05-23T00:00:00","2018-05-24T00:00:00","2018-05-25T00:00:00","2018-05-29T00:00:00","2018-05-30T00:00:00","2018-05-31T00:00:00","2018-06-01T00:00:00","2018-06-04T00:00:00","2018-06-05T00:00:00","2018-06-06T00:00:00","2018-06-07T00:00:00","2018-06-08T00:00:00","2018-06-11T00:00:00","2018-06-12T00:00:00","2018-06-13T00:00:00","2018-06-14T00:00:00","2018-06-15T00:00:00","2018-06-18T00:00:00","2018-06-19T00:00:00","2018-06-20T00:00:00","2018-06-21T00:00:00","2018-06-22T00:00:00","2018-06-25T00:00:00","2018-06-26T00:00:00","2018-06-27T00:00:00","2018-06-28T00:00:00","2018-06-29T00:00:00","2018-07-02T00:00:00","2018-07-03T00:00:00","2018-07-05T00:00:00","2018-07-06T00:00:00","2018-07-09T00:00:00","2018-07-10T00:00:00","2018-07-11T00:00:00","2018-07-12T00:00:00","2018-07-13T00:00:00","2018-07-16T00:00:00","2018-07-17T00:00:00","2018-07-18T00:00:00","2018-07-19T00:00:00","2018-07-20T00:00:00","2018-07-23T00:00:00","2018-07-24T00:00:00","2018-07-25T00:00:00","2018-07-26T00:00:00","2018-07-27T00:00:00","2018-07-30T00:00:00","2018-07-31T00:00:00","2018-08-01T00:00:00","2018-08-02T00:00:00","2018-08-03T00:00:00","2018-08-06T00:00:00","2018-08-07T00:00:00","2018-08-08T00:00:00","2018-08-09T00:00:00","2018-08-10T00:00:00","2018-08-13T00:00:00","2018-08-14T00:00:00","2018-08-15T00:00:00","2018-08-16T00:00:00","2018-08-17T00:00:00","2018-08-20T00:00:00","2018-08-21T00:00:00","2018-08-22T00:00:00","2018-08-23T00:00:00","2018-08-24T00:00:00","2018-08-27T00:00:00","2018-08-28T00:00:00","2018-08-29T00:00:00","2018-08-30T00:00:00","2018-08-31T00:00:00","2018-09-04T00:00:00","2018-09-05T00:00:00","2018-09-06T00:00:00","2018-09-07T00:00:00","2018-09-10T00:00:00","2018-09-11T00:00:00","2018-09-12T00:00:00","2018-09-13T00:00:00","2018-09-14T00:00:00","2018-09-17T00:00:00","2018-09-18T00:00:00","2018-09-19T00:00:00","2018-09-20T00:00:00","2018-09-21T00:00:00","2018-09-24T00:00:00","2018-09-25T00:00:00","2018-09-26T00:00:00","2018-09-27T00:00:00","2018-09-28T00:00:00","2018-10-01T00:00:00","2018-10-02T00:00:00","2018-10-03T00:00:00","2018-10-04T00:00:00","2018-10-05T00:00:00","2018-10-08T00:00:00","2018-10-09T00:00:00","2018-10-10T00:00:00","2018-10-11T00:00:00","2018-10-12T00:00:00","2018-10-15T00:00:00","2018-10-16T00:00:00","2018-10-17T00:00:00","2018-10-18T00:00:00","2018-10-19T00:00:00","2018-10-22T00:00:00","2018-10-23T00:00:00","2018-10-24T00:00:00","2018-10-25T00:00:00","2018-10-26T00:00:00","2018-10-29T00:00:00","2018-10-30T00:00:00","2018-10-31T00:00:00","2018-11-01T00:00:00","2018-11-02T00:00:00","2018-11-05T00:00:00","2018-11-06T00:00:00","2018-11-07T00:00:00","2018-11-08T00:00:00","2018-11-09T00:00:00","2018-11-12T00:00:00","2018-11-13T00:00:00","2018-11-14T00:00:00","2018-11-15T00:00:00","2018-11-16T00:00:00","2018-11-19T00:00:00","2018-11-20T00:00:00","2018-11-21T00:00:00","2018-11-23T00:00:00","2018-11-26T00:00:00","2018-11-27T00:00:00","2018-11-28T00:00:00","2018-11-29T00:00:00","2018-11-30T00:00:00","2018-12-03T00:00:00","2018-12-04T00:00:00","2018-12-06T00:00:00","2018-12-07T00:00:00","2018-12-10T00:00:00","2018-12-11T00:00:00","2018-12-12T00:00:00","2018-12-13T00:00:00","2018-12-14T00:00:00","2018-12-17T00:00:00","2018-12-18T00:00:00","2018-12-19T00:00:00","2018-12-20T00:00:00","2018-12-21T00:00:00","2018-12-24T00:00:00","2018-12-26T00:00:00","2018-12-27T00:00:00","2018-12-28T00:00:00","2018-12-31T00:00:00","2019-01-02T00:00:00","2019-01-03T00:00:00","2019-01-04T00:00:00","2019-01-07T00:00:00","2019-01-08T00:00:00","2019-01-09T00:00:00","2019-01-10T00:00:00","2019-01-11T00:00:00","2019-01-14T00:00:00","2019-01-15T00:00:00","2019-01-16T00:00:00","2019-01-17T00:00:00","2019-01-18T00:00:00","2019-01-22T00:00:00","2019-01-23T00:00:00","2019-01-24T00:00:00","2019-01-25T00:00:00","2019-01-28T00:00:00","2019-01-29T00:00:00","2019-01-30T00:00:00","2019-01-31T00:00:00","2019-02-01T00:00:00","2019-02-04T00:00:00","2019-02-05T00:00:00","2019-02-06T00:00:00","2019-02-07T00:00:00","2019-02-08T00:00:00","2019-02-11T00:00:00","2019-02-12T00:00:00","2019-02-13T00:00:00","2019-02-14T00:00:00","2019-02-15T00:00:00","2019-02-19T00:00:00","2019-02-20T00:00:00","2019-02-21T00:00:00","2019-02-22T00:00:00","2019-02-25T00:00:00","2019-02-26T00:00:00","2019-02-27T00:00:00","2019-02-28T00:00:00","2019-03-01T00:00:00","2019-03-04T00:00:00","2019-03-05T00:00:00","2019-03-06T00:00:00","2019-03-07T00:00:00","2019-03-08T00:00:00","2019-03-11T00:00:00","2019-03-12T00:00:00","2019-03-13T00:00:00","2019-03-14T00:00:00","2019-03-15T00:00:00","2019-03-18T00:00:00","2019-03-19T00:00:00","2019-03-20T00:00:00","2019-03-21T00:00:00","2019-03-22T00:00:00","2019-03-25T00:00:00","2019-03-26T00:00:00","2019-03-27T00:00:00","2019-03-28T00:00:00","2019-03-29T00:00:00","2019-04-01T00:00:00","2019-04-02T00:00:00","2019-04-03T00:00:00","2019-04-04T00:00:00","2019-04-05T00:00:00","2019-04-08T00:00:00","2019-04-09T00:00:00","2019-04-10T00:00:00","2019-04-11T00:00:00","2019-04-12T00:00:00","2019-04-15T00:00:00","2019-04-16T00:00:00","2019-04-17T00:00:00","2019-04-18T00:00:00","2019-04-22T00:00:00","2019-04-23T00:00:00","2019-04-24T00:00:00","2019-04-25T00:00:00","2019-04-26T00:00:00","2019-04-29T00:00:00","2019-04-30T00:00:00","2019-05-01T00:00:00","2019-05-02T00:00:00","2019-05-03T00:00:00","2019-05-06T00:00:00","2019-05-07T00:00:00","2019-05-08T00:00:00","2019-05-09T00:00:00","2019-05-10T00:00:00","2019-05-13T00:00:00","2019-05-14T00:00:00","2019-05-15T00:00:00","2019-05-16T00:00:00","2019-05-17T00:00:00","2019-05-20T00:00:00","2019-05-21T00:00:00","2019-05-22T00:00:00","2019-05-23T00:00:00","2019-05-24T00:00:00","2019-05-28T00:00:00","2019-05-29T00:00:00","2019-05-30T00:00:00","2019-05-31T00:00:00","2019-06-03T00:00:00","2019-06-04T00:00:00","2019-06-05T00:00:00","2019-06-06T00:00:00","2019-06-07T00:00:00","2019-06-10T00:00:00","2019-06-11T00:00:00","2019-06-12T00:00:00","2019-06-13T00:00:00","2019-06-14T00:00:00","2019-06-17T00:00:00","2019-06-18T00:00:00","2019-06-19T00:00:00","2019-06-20T00:00:00","2019-06-21T00:00:00","2019-06-24T00:00:00","2019-06-25T00:00:00","2019-06-26T00:00:00","2019-06-27T00:00:00","2019-06-28T00:00:00","2019-07-01T00:00:00","2019-07-02T00:00:00","2019-07-03T00:00:00","2019-07-05T00:00:00","2019-07-08T00:00:00","2019-07-09T00:00:00","2019-07-10T00:00:00","2019-07-11T00:00:00","2019-07-12T00:00:00","2019-07-15T00:00:00","2019-07-16T00:00:00","2019-07-17T00:00:00","2019-07-18T00:00:00","2019-07-19T00:00:00","2019-07-22T00:00:00","2019-07-23T00:00:00","2019-07-24T00:00:00","2019-07-25T00:00:00","2019-07-26T00:00:00","2019-07-29T00:00:00","2019-07-30T00:00:00","2019-07-31T00:00:00","2019-08-01T00:00:00","2019-08-02T00:00:00","2019-08-05T00:00:00","2019-08-06T00:00:00","2019-08-07T00:00:00","2019-08-08T00:00:00","2019-08-09T00:00:00","2019-08-12T00:00:00","2019-08-13T00:00:00","2019-08-14T00:00:00","2019-08-15T00:00:00","2019-08-16T00:00:00","2019-08-19T00:00:00","2019-08-20T00:00:00","2019-08-21T00:00:00","2019-08-22T00:00:00","2019-08-23T00:00:00","2019-08-26T00:00:00","2019-08-27T00:00:00","2019-08-28T00:00:00","2019-08-29T00:00:00","2019-08-30T00:00:00","2019-09-03T00:00:00","2019-09-04T00:00:00","2019-09-05T00:00:00","2019-09-06T00:00:00","2019-09-09T00:00:00","2019-09-10T00:00:00","2019-09-11T00:00:00","2019-09-12T00:00:00","2019-09-13T00:00:00","2019-09-16T00:00:00","2019-09-17T00:00:00","2019-09-18T00:00:00","2019-09-19T00:00:00","2019-09-20T00:00:00","2019-09-23T00:00:00","2019-09-24T00:00:00","2019-09-25T00:00:00","2019-09-26T00:00:00","2019-09-27T00:00:00","2019-09-30T00:00:00","2019-10-01T00:00:00","2019-10-02T00:00:00","2019-10-03T00:00:00","2019-10-04T00:00:00","2019-10-07T00:00:00","2019-10-08T00:00:00","2019-10-09T00:00:00","2019-10-10T00:00:00","2019-10-11T00:00:00","2019-10-14T00:00:00","2019-10-15T00:00:00","2019-10-16T00:00:00","2019-10-17T00:00:00","2019-10-18T00:00:00","2019-10-21T00:00:00","2019-10-22T00:00:00","2019-10-23T00:00:00","2019-10-24T00:00:00","2019-10-25T00:00:00","2019-10-28T00:00:00","2019-10-29T00:00:00","2019-10-30T00:00:00","2019-10-31T00:00:00","2019-11-01T00:00:00","2019-11-04T00:00:00","2019-11-05T00:00:00","2019-11-06T00:00:00","2019-11-07T00:00:00","2019-11-08T00:00:00","2019-11-11T00:00:00","2019-11-12T00:00:00","2019-11-13T00:00:00","2019-11-14T00:00:00","2019-11-15T00:00:00","2019-11-18T00:00:00","2019-11-19T00:00:00","2019-11-20T00:00:00","2019-11-21T00:00:00","2019-11-22T00:00:00","2019-11-25T00:00:00","2019-11-26T00:00:00","2019-11-27T00:00:00","2019-11-29T00:00:00","2019-12-02T00:00:00","2019-12-03T00:00:00","2019-12-04T00:00:00","2019-12-05T00:00:00","2019-12-06T00:00:00","2019-12-09T00:00:00","2019-12-10T00:00:00","2019-12-11T00:00:00","2019-12-12T00:00:00","2019-12-13T00:00:00","2019-12-16T00:00:00","2019-12-17T00:00:00","2019-12-18T00:00:00","2019-12-19T00:00:00","2019-12-20T00:00:00","2019-12-23T00:00:00","2019-12-24T00:00:00","2019-12-26T00:00:00","2019-12-27T00:00:00","2019-12-30T00:00:00","2019-12-31T00:00:00","2020-01-02T00:00:00","2020-01-03T00:00:00","2020-01-06T00:00:00","2020-01-07T00:00:00","2020-01-08T00:00:00","2020-01-09T00:00:00","2020-01-10T00:00:00","2020-01-13T00:00:00","2020-01-14T00:00:00","2020-01-15T00:00:00","2020-01-16T00:00:00","2020-01-17T00:00:00","2020-01-21T00:00:00","2020-01-22T00:00:00","2020-01-23T00:00:00","2020-01-24T00:00:00","2020-01-27T00:00:00","2020-01-28T00:00:00","2020-01-29T00:00:00","2020-01-30T00:00:00","2020-01-31T00:00:00","2020-02-03T00:00:00","2020-02-04T00:00:00","2020-02-05T00:00:00","2020-02-06T00:00:00","2020-02-07T00:00:00","2020-02-10T00:00:00","2020-02-11T00:00:00","2020-02-12T00:00:00","2020-02-13T00:00:00","2020-02-14T00:00:00","2020-02-18T00:00:00","2020-02-19T00:00:00","2020-02-20T00:00:00","2020-02-21T00:00:00","2020-02-24T00:00:00","2020-02-25T00:00:00","2020-02-26T00:00:00","2020-02-27T00:00:00","2020-02-28T00:00:00","2020-03-02T00:00:00","2020-03-03T00:00:00","2020-03-04T00:00:00","2020-03-05T00:00:00","2020-03-06T00:00:00","2020-03-09T00:00:00","2020-03-10T00:00:00","2020-03-11T00:00:00","2020-03-12T00:00:00","2020-03-13T00:00:00","2020-03-16T00:00:00","2020-03-17T00:00:00","2020-03-18T00:00:00","2020-03-19T00:00:00","2020-03-20T00:00:00","2020-03-23T00:00:00","2020-03-24T00:00:00","2020-03-25T00:00:00","2020-03-26T00:00:00","2020-03-27T00:00:00","2020-03-30T00:00:00","2020-03-31T00:00:00","2020-04-01T00:00:00","2020-04-02T00:00:00","2020-04-03T00:00:00","2020-04-06T00:00:00","2020-04-07T00:00:00","2020-04-08T00:00:00","2020-04-09T00:00:00","2020-04-13T00:00:00","2020-04-14T00:00:00","2020-04-15T00:00:00","2020-04-16T00:00:00","2020-04-17T00:00:00","2020-04-20T00:00:00","2020-04-21T00:00:00","2020-04-22T00:00:00","2020-04-23T00:00:00","2020-04-24T00:00:00","2020-04-27T00:00:00","2020-04-28T00:00:00","2020-04-29T00:00:00","2020-04-30T00:00:00","2020-05-01T00:00:00","2020-05-04T00:00:00","2020-05-05T00:00:00","2020-05-06T00:00:00","2020-05-07T00:00:00","2020-05-08T00:00:00","2020-05-11T00:00:00","2020-05-12T00:00:00","2020-05-13T00:00:00","2020-05-14T00:00:00","2020-05-15T00:00:00","2020-05-18T00:00:00","2020-05-19T00:00:00","2020-05-20T00:00:00","2020-05-21T00:00:00","2020-05-22T00:00:00","2020-05-26T00:00:00","2020-05-27T00:00:00","2020-05-28T00:00:00","2020-05-29T00:00:00","2020-06-01T00:00:00","2020-06-02T00:00:00","2020-06-03T00:00:00","2020-06-04T00:00:00","2020-06-05T00:00:00","2020-06-08T00:00:00","2020-06-09T00:00:00","2020-06-10T00:00:00","2020-06-11T00:00:00","2020-06-12T00:00:00","2020-06-15T00:00:00","2020-06-16T00:00:00","2020-06-17T00:00:00","2020-06-18T00:00:00","2020-06-19T00:00:00","2020-06-22T00:00:00","2020-06-23T00:00:00","2020-06-24T00:00:00","2020-06-25T00:00:00","2020-06-26T00:00:00","2020-06-29T00:00:00","2020-06-30T00:00:00","2020-07-01T00:00:00","2020-07-02T00:00:00","2020-07-06T00:00:00","2020-07-07T00:00:00","2020-07-08T00:00:00","2020-07-09T00:00:00","2020-07-10T00:00:00","2020-07-13T00:00:00","2020-07-14T00:00:00","2020-07-15T00:00:00","2020-07-16T00:00:00","2020-07-17T00:00:00","2020-07-20T00:00:00","2020-07-21T00:00:00","2020-07-22T00:00:00","2020-07-23T00:00:00","2020-07-24T00:00:00","2020-07-27T00:00:00","2020-07-28T00:00:00","2020-07-29T00:00:00","2020-07-30T00:00:00","2020-07-31T00:00:00","2020-08-03T00:00:00","2020-08-04T00:00:00","2020-08-05T00:00:00","2020-08-06T00:00:00","2020-08-07T00:00:00","2020-08-10T00:00:00","2020-08-11T00:00:00","2020-08-12T00:00:00","2020-08-13T00:00:00","2020-08-14T00:00:00","2020-08-17T00:00:00","2020-08-18T00:00:00","2020-08-19T00:00:00","2020-08-20T00:00:00","2020-08-21T00:00:00","2020-08-24T00:00:00","2020-08-25T00:00:00","2020-08-26T00:00:00","2020-08-27T00:00:00","2020-08-28T00:00:00","2020-08-31T00:00:00","2020-09-01T00:00:00","2020-09-02T00:00:00","2020-09-03T00:00:00","2020-09-04T00:00:00","2020-09-08T00:00:00","2020-09-09T00:00:00","2020-09-10T00:00:00","2020-09-11T00:00:00","2020-09-14T00:00:00","2020-09-15T00:00:00","2020-09-16T00:00:00","2020-09-17T00:00:00","2020-09-18T00:00:00","2020-09-21T00:00:00","2020-09-22T00:00:00","2020-09-23T00:00:00","2020-09-24T00:00:00","2020-09-25T00:00:00","2020-09-28T00:00:00","2020-09-29T00:00:00","2020-09-30T00:00:00","2020-10-01T00:00:00","2020-10-02T00:00:00","2020-10-05T00:00:00","2020-10-06T00:00:00","2020-10-07T00:00:00","2020-10-08T00:00:00","2020-10-09T00:00:00","2020-10-12T00:00:00","2020-10-13T00:00:00","2020-10-14T00:00:00","2020-10-15T00:00:00","2020-10-16T00:00:00","2020-10-19T00:00:00","2020-10-20T00:00:00","2020-10-21T00:00:00","2020-10-22T00:00:00","2020-10-23T00:00:00","2020-10-26T00:00:00","2020-10-27T00:00:00","2020-10-28T00:00:00","2020-10-29T00:00:00","2020-10-30T00:00:00","2020-11-02T00:00:00","2020-11-03T00:00:00","2020-11-04T00:00:00","2020-11-05T00:00:00","2020-11-06T00:00:00","2020-11-09T00:00:00","2020-11-10T00:00:00","2020-11-11T00:00:00","2020-11-12T00:00:00","2020-11-13T00:00:00","2020-11-16T00:00:00","2020-11-17T00:00:00","2020-11-18T00:00:00","2020-11-19T00:00:00","2020-11-20T00:00:00","2020-11-23T00:00:00","2020-11-24T00:00:00","2020-11-25T00:00:00","2020-11-27T00:00:00","2020-11-30T00:00:00","2020-12-01T00:00:00","2020-12-02T00:00:00","2020-12-03T00:00:00","2020-12-04T00:00:00","2020-12-07T00:00:00","2020-12-08T00:00:00","2020-12-09T00:00:00","2020-12-10T00:00:00","2020-12-11T00:00:00","2020-12-14T00:00:00","2020-12-15T00:00:00","2020-12-16T00:00:00","2020-12-17T00:00:00","2020-12-18T00:00:00","2020-12-21T00:00:00","2020-12-22T00:00:00","2020-12-23T00:00:00","2020-12-24T00:00:00","2020-12-28T00:00:00","2020-12-29T00:00:00","2020-12-30T00:00:00","2020-12-31T00:00:00","2021-01-04T00:00:00","2021-01-05T00:00:00","2021-01-06T00:00:00","2021-01-07T00:00:00","2021-01-08T00:00:00","2021-01-11T00:00:00","2021-01-12T00:00:00","2021-01-13T00:00:00","2021-01-14T00:00:00","2021-01-15T00:00:00","2021-01-19T00:00:00","2021-01-20T00:00:00","2021-01-21T00:00:00","2021-01-22T00:00:00","2021-01-25T00:00:00","2021-01-26T00:00:00","2021-01-27T00:00:00","2021-01-28T00:00:00","2021-01-29T00:00:00","2021-02-01T00:00:00","2021-02-02T00:00:00","2021-02-03T00:00:00","2021-02-04T00:00:00","2021-02-05T00:00:00","2021-02-08T00:00:00","2021-02-09T00:00:00","2021-02-10T00:00:00","2021-02-11T00:00:00","2021-02-12T00:00:00","2021-02-16T00:00:00","2021-02-17T00:00:00","2021-02-18T00:00:00","2021-02-19T00:00:00","2021-02-22T00:00:00","2021-02-23T00:00:00","2021-02-24T00:00:00","2021-02-25T00:00:00","2021-02-26T00:00:00","2021-03-01T00:00:00","2021-03-02T00:00:00","2021-03-03T00:00:00","2021-03-04T00:00:00","2021-03-05T00:00:00","2021-03-08T00:00:00","2021-03-09T00:00:00","2021-03-10T00:00:00","2021-03-11T00:00:00","2021-03-12T00:00:00","2021-03-15T00:00:00","2021-03-16T00:00:00","2021-03-17T00:00:00","2021-03-18T00:00:00","2021-03-19T00:00:00","2021-03-22T00:00:00","2021-03-23T00:00:00","2021-03-24T00:00:00","2021-03-25T00:00:00","2021-03-26T00:00:00","2021-03-29T00:00:00","2021-03-30T00:00:00","2021-03-31T00:00:00","2021-04-01T00:00:00","2021-04-05T00:00:00","2021-04-06T00:00:00","2021-04-07T00:00:00","2021-04-08T00:00:00","2021-04-09T00:00:00","2021-04-12T00:00:00","2021-04-13T00:00:00","2021-04-14T00:00:00","2021-04-15T00:00:00","2021-04-16T00:00:00","2021-04-19T00:00:00","2021-04-20T00:00:00","2021-04-21T00:00:00","2021-04-22T00:00:00","2021-04-23T00:00:00","2021-04-26T00:00:00","2021-04-27T00:00:00","2021-04-28T00:00:00","2021-04-29T00:00:00","2021-04-30T00:00:00","2021-05-03T00:00:00","2021-05-04T00:00:00","2021-05-05T00:00:00","2021-05-06T00:00:00","2021-05-07T00:00:00","2021-05-10T00:00:00","2021-05-11T00:00:00","2021-05-12T00:00:00","2021-05-13T00:00:00","2021-05-14T00:00:00","2021-05-17T00:00:00","2021-05-18T00:00:00","2021-05-19T00:00:00","2021-05-20T00:00:00","2021-05-21T00:00:00","2021-05-24T00:00:00","2021-05-25T00:00:00","2021-05-26T00:00:00","2021-05-27T00:00:00","2021-05-28T00:00:00","2021-06-01T00:00:00","2021-06-02T00:00:00","2021-06-03T00:00:00","2021-06-04T00:00:00","2021-06-07T00:00:00","2021-06-08T00:00:00","2021-06-09T00:00:00","2021-06-10T00:00:00","2021-06-11T00:00:00","2021-06-14T00:00:00"],"y":[1.5926669836044312,1.5886670351028442,1.4639999866485596,1.2799999713897705,1.0740000009536743,1.053333044052124,1.1640000343322754,1.159999966621399,1.136667013168335,1.2093329429626465,1.3226670026779175,1.3259999752044678,1.3760000467300415,1.4606670141220093,1.3533329963684082,1.3480000495910645,1.399999976158142,1.4193329811096191,1.3966670036315918,1.3700000047683716,1.3813329935073853,1.3566670417785645,1.329332947731018,1.3946670293807983,1.463333010673523,1.4173330068588257,1.363332986831665,1.305999994277954,1.3066669702529907,1.2686669826507568,1.1933330297470093,1.1733330488204956,1.2213330268859863,1.2519999742507935,1.2766669988632202,1.2513329982757568,1.25266695022583,1.273332953453064,1.3420000076293945,1.2799999713897705,1.3266669511795044,1.3166669607162476,1.3133330345153809,1.324666976928711,1.2986669540405273,1.363332986831665,1.4040000438690186,1.4033329486846924,1.369333028793335,1.3933329582214355,1.380666971206665,1.3446669578552246,1.3813329935073853,1.4079999923706055,1.4653329849243164,1.3960000276565552,1.348667025566101,1.4040000438690186,1.3846670389175415,1.324666976928711,1.3040000200271606,1.340000033378601,1.3686670064926147,1.4266669750213623,1.4653329849243164,1.3606669902801514,1.3733329772949219,1.3993330001831055,1.4079999923706055,1.3639999628067017,1.3619999885559082,1.3619999885559082,1.3493330478668213,1.3493330478668213,1.369333028793335,1.3833329677581787,1.369333028793335,1.348667025566101,1.3366669416427612,1.3766670227050781,1.3833329677581787,1.3813329935073853,1.3899999856948853,1.4240000247955322,1.399999976158142,1.4126670360565186,1.4559999704360962,1.4273329973220825,1.4166669845581055,1.4513330459594727,1.659999966621399,1.6293330192565918,1.6653330326080322,1.6419999599456787,1.957332968711853,1.869333028793335,1.9893330335617065,2.053333044052124,1.9780000448226929,1.965999960899353,1.9926669597625732,2.065999984741211,2.2266669273376465,2.3046669960021973,2.3646669387817383,2.3546669483184814,2.2886669635772705,2.355333089828491,2.2899999618530273,2.1566669940948486,2.0993330478668213,2.02066707611084,2.1040000915527344,2.1579999923706055,2.136667013168335,2.101332902908325,2.0366671085357666,1.9019999504089355,1.9733330011367798,2.053999900817871,2.0906670093536377,2.113332986831665,2.1506669521331787,2.175333023071289,2.00600004196167,1.7033330202102661,1.7606669664382935,1.848667025566101,1.7666670083999634,1.775333046913147,1.7746670246124268,1.777999997138977,1.7886669635772705,1.858667016029358,1.8826669454574585,1.8966670036315918,1.797333002090454,1.797333002090454,1.7480000257492065,1.7166670560836792,1.7093329429626465,1.6019999980926514,1.5080000162124634,1.5360000133514404,1.6326669454574585,1.6453330516815186,1.649999976158142,1.6613329648971558,1.6006669998168945,1.6066670417785645,1.593999981880188,1.5959999561309814,1.5753329992294312,1.5640000104904175,1.5379999876022339,1.6326669454574585,1.547333002090454,1.5479999780654907,1.5499999523162842,1.5386669635772705,1.5226670503616333,1.6486669778823853,1.5733330249786377,1.5453330278396606,1.4579999446868896,1.4553329944610596,1.5019999742507935,1.5740000009536743,1.5926669836044312,1.5959999561309814,1.6013330221176147,1.6239999532699585,1.6633330583572388,1.6626670360565186,1.6440000534057617,1.6480000019073486,1.6006669998168945,1.6046669483184814,1.5499999523162842,1.5299999713897705,1.5213329792022705,1.5206669569015503,1.5306669473648071,1.5153330564498901,1.4793330430984497,1.480666995048523,1.4886670112609863,1.5166670083999634,1.5499999523162842,1.5946669578552246,1.5806670188903809,1.850000023841858,1.7773330211639404,1.722000002861023,1.7799999713897705,1.7660000324249268,1.815999984741211,1.7660000324249268,1.6846669912338257,1.6433329582214355,1.6619999408721924,1.6759999990463257,1.7053329944610596,1.668666958808899,1.6773329973220825,1.7166670560836792,1.7826670408248901,1.7593330144882202,1.7953330278396606,1.8053330183029175,1.843999981880188,1.840000033378601,1.8300000429153442,1.7913329601287842,1.7793329954147339,1.762666940689087,1.8079999685287476,1.8606669902801514,1.8886669874191284,1.8046669960021973,1.8446669578552246,1.8366669416427612,1.773332953453064,1.730666995048523,1.7566670179367065,1.8799999952316284,1.8646670579910278,1.7879999876022339,1.7813329696655273,1.9320000410079956,1.9653329849243164,1.9700000286102295,2.0093328952789307,1.901332974433899,1.9173330068588257,2.0086669921875,1.9133330583572388,1.891332983970642,1.8079999685287476,1.841333031654358,1.8573329448699951,1.8953330516815186,1.9066669940948486,1.8213330507278442,1.7666670083999634,1.7666670083999634,1.7339999675750732,1.835332989692688,1.8140000104904175,1.8473329544067383,1.8380000591278076,1.8306670188903809,1.8739999532699585,1.8860000371932983,1.9420000314712524,1.9346669912338257,1.942667007446289,1.9306670427322388,1.9819999933242798,1.920667052268982,1.8899999856948853,1.878000020980835,1.9093329906463623,1.8406670093536377,1.8386670351028442,1.8153330087661743,1.8593330383300781,1.9126670360565186,1.9133330583572388,1.952666997909546,1.8993330001831055,1.8666670322418213,1.8426669836044312,1.878000020980835,1.878000020980835,1.9179999828338623,1.8226670026779175,1.8133330345153809,1.649999976158142,1.6160000562667847,1.5759999752044678,1.670667052268982,1.5880000591278076,1.6866669654846191,1.753999948501587,1.7486670017242432,1.7400000095367432,1.722000002861023,1.6173330545425415,1.4866670370101929,1.463333010673523,1.5306669473648071,1.591333031654358,1.5406670570373535,1.5820000171661377,1.647333025932312,1.6419999599456787,1.6493330001831055,1.600000023841858,1.5379999876022339,1.5293329954147339,1.5893330574035645,1.5740000009536743,1.5313329696655273,1.525333046913147,1.6053329706192017,1.6226669549942017,1.6546670198440552,1.7200000286102295,1.718000054359436,1.7339999675750732,1.7233330011367798,1.7086670398712158,1.7586669921875,1.7013330459594727,1.746000051498413,1.6393330097198486,1.6080000400543213,1.6260000467300415,1.5820000171661377,1.5773329734802246,1.6913330554962158,1.797333002090454,1.7993329763412476,1.858667016029358,1.8406670093536377,1.8533329963684082,1.8626669645309448,1.8700000047683716,1.8279999494552612,1.8893330097198486,1.8380000591278076,1.8226670026779175,1.8686670064926147,1.9033329486846924,1.8833329677581787,1.8653329610824585,1.9173330068588257,1.9913330078125,1.9579999446868896,1.925333023071289,1.9140000343322754,2.1640000343322754,2.1540000438690186,2.0846669673919678,2.122667074203491,2.058666944503784,2.0886669158935547,2.2426669597625732,2.2146670818328857,2.26200008392334,2.3293330669403076,2.245332956314087,2.173332929611206,2.117332935333252,2.138000011444092,2.0966670513153076,2.1106669902801514,2.1706669330596924,2.1166670322418213,2.1826670169830322,2.173332929611206,2.2200000286102295,2.2946670055389404,2.324666976928711,2.2793331146240234,2.059333086013794,2.069333076477051,2.0273330211639404,1.963333010673523,1.9019999504089355,1.9079999923706055,1.8666670322418213,1.850000023841858,1.8600000143051147,1.8380000591278076,1.8513330221176147,1.8600000143051147,1.9046670198440552,1.9006669521331787,1.9153330326080322,1.9040000438690186,1.871999979019165,1.8473329544067383,1.8079999685287476,1.7940000295639038,1.8166669607162476,1.841333031654358,1.8819999694824219,1.8833329677581787,1.519333004951477,1.773332953453064,1.7873330116271973,1.784000039100647,1.773332953453064,1.7846670150756836,1.8279999494552612,1.8646670579910278,1.929332971572876,1.9553329944610596,1.9713330268859863,1.937999963760376,1.972000002861023,2.016666889190674,2.076667070388794,2.119999885559082,2.1066670417785645,2.128667116165161,2.171999931335449,2.0733330249786377,2.0993330478668213,2.2113330364227295,2.240000009536743,2.2786669731140137,2.3313329219818115,2.299999952316284,2.2813329696655273,2.302000045776367,2.25,2.2413330078125,2.253999948501587,2.2273330688476562,2.2939999103546143,2.2693328857421875,2.251332998275757,2.2073330879211426,2.2079999446868896,2.204667091369629,2.315999984741211,2.4006669521331787,2.4059998989105225,2.3526670932769775,2.3333330154418945,2.3546669483184814,2.3320000171661377,2.330667018890381,2.3433330059051514,2.293333053588867,2.2720000743865967,2.493333101272583,2.5293331146240234,2.5233330726623535,2.4886670112609863,2.4826669692993164,2.438667058944702,2.5339999198913574,2.3333330154418945,2.2986669540405273,2.2100000381469727,2.1640000343322754,2.2060000896453857,2.22933292388916,2.239332914352417,2.1500000953674316,2.1493330001831055,2.177333116531372,2.2106668949127197,2.2106668949127197,2.129333019256592,2.121332883834839,2.194000005722046,2.2326669692993164,2.2226669788360596,2.208667039871216,2.252000093460083,2.262666940689087,2.1640000343322754,2.121999979019165,2.1646668910980225,2.012666940689087,2.003999948501587,2.1973330974578857,2.1500000953674316,2.003999948501587,1.9620000123977661,1.9453330039978027,1.9046670198440552,1.8373329639434814,1.9179999828338623,2.053333044052124,2.068000078201294,2.018666982650757,1.987333059310913,2.1126670837402344,2.0273330211639404,1.9666670560836792,1.8766670227050781,1.858667016029358,1.8606669902801514,1.9479999542236328,1.9286669492721558,2.0053329467773438,1.9413330554962158,1.9773329496383667,1.9846669435501099,1.9593329429626465,1.99399995803833,2.122667074203491,2.1393330097198486,2.252000093460083,2.1459999084472656,2.25266695022583,2.2073330879211426,2.107332944869995,2.130666971206665,2.0940001010894775,2.0859999656677246,2.0266671180725098,2.0439999103546143,2.0820000171661377,2.065999984741211,2.0993330478668213,2.0846669673919678,2.1006669998168945,2.180000066757202,2.2833330631256104,2.3973329067230225,2.2233328819274902,2.1433329582214355,2.1513330936431885,2.119333028793335,2.0439999103546143,1.9893330335617065,1.9299999475479126,1.8753329515457153,1.9673329591751099,1.8233330249786377,1.8279999494552612,1.75,1.7400000095367432,1.8179999589920044,1.8846670389175415,2.016666889190674,1.9393329620361328,1.9606670141220093,1.996000051498413,2.078000068664551,1.9613330364227295,1.9600000381469727,2.0199999809265137,2.000667095184326,1.9673329591751099,1.9406670331954956,1.9966670274734497,2.0486669540405273,1.9666670560836792,1.8880000114440918,1.9126670360565186,1.8940000534057617,1.8940000534057617,1.901332974433899,1.8760000467300415,1.8626669645309448,1.9033329486846924,1.9566669464111328,1.824666976928711,1.8533329963684082,1.8853329420089722,1.9653329849243164,2.0260000228881836,2.169332981109619,2.0893330574035645,2.069999933242798,2.059999942779541,2.001332998275757,2.0439999103546143,1.843999981880188,1.8359999656677246,1.8993330001831055,1.9520000219345093,1.944000005722046,1.9866670370101929,1.9533330202102661,1.9600000381469727,1.9259999990463257,1.9500000476837158,1.891332983970642,1.8933329582214355,1.8880000114440918,1.8426669836044312,1.8220000267028809,1.8706669807434082,1.9213329553604126,1.869333028793335,1.8493330478668213,1.8566670417785645,1.8926670551300049,1.8279999494552612,1.8346669673919678,1.8253329992294312,1.8753329515457153,1.9500000476837158,1.9279999732971191,2.0999999046325684,2.076667070388794,2.1026670932769775,2.0873329639434814,2.0213329792022705,2.0713329315185547,2.107332944869995,2.0920000076293945,2.0546669960021973,2.122667074203491,2.194667100906372,2.200000047683716,2.1646668910980225,2.1419999599456787,2.1513330936431885,2.1433329582214355,2.2153329849243164,2.246000051498413,2.254667043685913,2.308000087738037,2.259999990463257,2.24733304977417,2.259999990463257,2.2780001163482666,2.3046669960021973,2.3519999980926514,2.3506669998168945,2.2406671047210693,2.253999948501587,2.293333053588867,2.305999994277954,2.307332992553711,2.295332908630371,2.266666889190674,2.2853329181671143,2.239332914352417,2.246000051498413,2.2146670818328857,2.257999897003174,2.357332944869995,2.318000078201294,2.293333053588867,2.2893331050872803,2.245332956314087,2.2426669597625732,2.23533296585083,2.194000005722046,2.2173330783843994,2.259999990463257,2.2733330726623535,2.2920000553131104,2.301332950592041,2.3459999561309814,2.4000000953674316,2.4660000801086426,2.4653329849243164,2.5353329181671143,2.5299999713897705,2.501332998275757,2.500667095184326,2.553333044052124,2.5160000324249268,2.5420000553131104,2.611332893371582,2.631999969482422,2.615999937057495,2.561332941055298,2.5260000228881836,2.563333034515381,2.551332950592041,2.4693329334259033,2.618666887283325,2.569333076477051,2.3440001010894775,2.4073328971862793,2.2920000553131104,2.295332908630371,2.3399999141693115,2.322000026702881,2.309999942779541,2.371999979019165,2.4433329105377197,2.512666940689087,2.5486669540405273,2.564666986465454,2.6066670417785645,2.6080000400543213,2.5986669063568115,2.456666946411133,2.3526670932769775,2.3433330059051514,2.3386669158935547,2.396667003631592,2.4006669521331787,2.441333055496216,2.502000093460083,2.5239999294281006,2.5439999103546143,2.5260000228881836,2.9286670684814453,2.9560000896453857,2.740000009536743,2.8006670475006104,2.757999897003174,2.7886669635772705,2.700000047683716,2.7906670570373535,2.9059998989105225,2.9166669845581055,2.886667013168335,3.0393331050872803,3.0299999713897705,3.131333112716675,3.188667058944702,3.3459999561309814,3.4006669521331787,3.361999988555908,3.4666669368743896,3.413332939147949,3.6626670360565186,3.5993330478668213,3.552000045776367,3.607332944869995,3.636667013168335,3.9666669368743896,3.700666904449463,3.7193329334259033,4.626667022705078,5.117332935333252,5.853332996368408,5.549333095550537,5.656000137329102,6.150000095367432,6.099999904632568,5.995999813079834,5.8393330574035645,5.815999984741211,6.182000160217285,6.4720001220703125,7.355332851409912,6.975333213806152,6.99666690826416,6.517333030700684,6.172667026519775,6.322667121887207,6.357999801635742,6.489999771118164,6.802667140960693,6.670000076293945,6.297999858856201,6.51533317565918,6.545332908630371,6.686666965484619,6.813333034515381,6.892666816711426,6.97866678237915,6.710000038146973,6.636666774749756,6.765999794006348,6.826666831970215,7.047999858856201,7.283332824707031,7.157332897186279,7.811999797821045,7.8546671867370605,7.682666778564453,8.005999565124512,8.107333183288574,8.229999542236328,8.15133285522461,8.37399959564209,8.65999984741211,8.484000205993652,7.269999980926514,8.016667366027832,7.935332775115967,7.97866678237915,8.161999702453613,8.182666778564453,8.113332748413086,8.271332740783691,8.62600040435791,8.974666595458984,8.78266716003418,8.95199966430664,9.036666870117188,9.199999809265137,9.645333290100098,9.476667404174805,8.9486665725708,10.232000350952148,10.199999809265137,9.825332641601562,9.695332527160645,9.290666580200195,9.311332702636719,9.466667175292969,9.65999984741211,9.972000122070312,9.857333183288574,10.473333358764648,10.78933334350586,10.947999954223633,11.133999824523926,11.096667289733887,11.070667266845703,11.266667366027832,11.262666702270508,11.374667167663574,11.328666687011719,11.131333351135254,10.713333129882812,11.091333389282227,10.90133285522461,10.995332717895508,11.03600025177002,11.10533332824707,11.081999778747559,11.08133316040039,11.861332893371582,12.22599983215332,12.074000358581543,12.155332565307617,12.349332809448242,12.576000213623047,12.726667404174805,12.891332626342773,12.866666793823242,12.063332557678223,11.553999900817871,12.065333366394043,12.204667091369629,11.648667335510254,11.251999855041504,11.528667449951172,11.91333293914795,11.981332778930664,12.262666702270508,12.237333297729492,12.186667442321777,12.226667404174805,11.506667137145996,11.435999870300293,10.966667175292969,11.543333053588867,11.310667037963867,10.857333183288574,10.964667320251465,10.614666938781738,10.662667274475098,10.811332702636719,11.680000305175781,11.787332534790039,10.077333450317383,9.317999839782715,9.196666717529297,9.646666526794434,9.186667442321777,9.24666690826416,9.173333168029785,9.029999732971191,8.10533332824707,8.406000137329102,8.074000358581543,8.140000343322754,8.092000007629395,8.055999755859375,8.033332824707031,8.462667465209961,8.485333442687988,8.277999877929688,9.646666526794434,9.263333320617676,9.36533260345459,9.157333374023438,9.4399995803833,9.47933292388916,9.3100004196167,9.83133316040039,9.84333324432373,9.862667083740234,10.163999557495117,9.86533260345459,9.381333351135254,9.549332618713379,9.569999694824219,10.093999862670898,10.366666793823242,10.074666976928711,10.162667274475098,10.028667449951172,10.006667137145996,9.970666885375977,9.800000190734863,9.957332611083984,10.085332870483398,9.835332870483398,9.714667320251465,9.28933334350586,10.751333236694336,10.942000389099121,11.39799976348877,11.333999633789062,11.778667449951172,11.904000282287598,12.100000381469727,11.640000343322754,11.307999610900879,11.892000198364258,11.682000160217285,12.189332962036133,12.093999862670898,11.807332992553711,11.915332794189453,11.628000259399414,11.892000198364258,12.435333251953125,13.104000091552734,13.107999801635742,13.021332740783691,13.308667182922363,13.215332984924316,13.579999923706055,12.909333229064941,13.998000144958496,13.973333358764648,14.510000228881836,16.53333282470703,16.866666793823242,16.836000442504883,16.320667266845703,16.70400047302246,16.98933219909668,16.8439998626709,16.862667083740234,16.413999557495117,15.922666549682617,15.62733268737793,16.099332809448242,15.852666854858398,15.39799976348877,15.59866714477539,16.002666473388672,15.72266674041748,15.660667419433594,15.259332656860352,14.678000450134277,14.696000099182129,14.197333335876465,13.821332931518555,14.157999992370605,13.896666526794434,14.464667320251465,15.352666854858398,15.026666641235352,14.148667335510254,13.834667205810547,14.36400032043457,14.461999893188477,13.612667083740234,13.585332870483398,13.206000328063965,12.927332878112793,13.27400016784668,13.208000183105469,13.625332832336426,14.576000213623047,13.866000175476074,13.857333183288574,13.323332786560059,13.234000205993652,13.79466724395752,13.859333038330078,13.84866714477539,14.060667037963867,14.440667152404785,13.8186674118042,13.423333168029785,11.906000137329102,12.150667190551758,12.311332702636719,12.677332878112793,12.708000183105469,12.572667121887207,12.77066707611084,13.072667121887207,13.020000457763672,13.296667098999023,13.658666610717773,13.819999694824219,14.104000091552734,14.015999794006348,14.015999794006348,13.851332664489746,13.646666526794434,13.662667274475098,13.599332809448242,13.793333053588867,13.878000259399414,13.687333106994629,13.486666679382324,13.631333351135254,13.567999839782715,13.761333465576172,14.973999977111816,15.444666862487793,15.141332626342773,15.185999870300293,15.305999755859375,15.814666748046875,15.5,15.792667388916016,15.706666946411133,15.937333106994629,16.003999710083008,15.981332778930664,15.295332908630371,15.283332824707031,14.843999862670898,14.604666709899902,14.870667457580566,14.630666732788086,14.541999816894531,15.113332748413086,14.638667106628418,14.477333068847656,14.359999656677246,14.668000221252441,14.702667236328125,14.638667106628418,14.832667350769043,14.902667045593262,14.904666900634766,14.98799991607666,15.000666618347168,15.261333465576172,14.886667251586914,15.5513334274292,15.90133285522461,15.899333000183105,16.595333099365234,16.826000213623047,16.54199981689453,17.288000106811523,17.33066749572754,17.354000091552734,17.42533302307129,17.46733283996582,17.32933235168457,17.117332458496094,17.047332763671875,16.95599937438965,17.118667602539062,17.503332138061523,17.44933319091797,17.549999237060547,17.590667724609375,17.979999542236328,18.941333770751953,18.746000289916992,19.069332122802734,18.492666244506836,18.80733299255371,18.565332412719727,18.739999771118164,18.687332153320312,18.613332748413086,16.923999786376953,17.382667541503906,17.42533302307129,17.58799934387207,17.288000106811523,16.66866683959961,16.694000244140625,16.80933380126953,16.463333129882812,16.440000534057617,16.35066795349121,16.178667068481445,16.016000747680664,16.761333465576172,17.013999938964844,17.374666213989258,17.30466651916504,17.28533363342285,17.134000778198242,15.793999671936035,14.97266674041748,15.137332916259766,15.313332557678223,15.09000015258789,15.165332794189453,15.364666938781738,15.689332962036133,15.40666675567627,15.685999870300293,15.682666778564453,14.777999877929688,16.184667587280273,15.873332977294922,15.910667419433594,16.113332748413086,16.172666549682617,15.928667068481445,15.39799976348877,16.08133316040039,16.01333236694336,16.1286678314209,16.738666534423828,16.606666564941406,16.780000686645508,17.245332717895508,16.93199920654297,17.18000030517578,16.516000747680664,16.58066749572754,16.185333251953125,16.447999954223633,16.53933334350586,16.562667846679688,16.301332473754883,15.442667007446289,15.428667068481445,15.286666870117188,15.218667030334473,14.913999557495117,14.290666580200195,14.459333419799805,13.989333152770996,13.925333023071289,13.800000190734863,13.602666854858398,13.187333106994629,13.721332550048828,14.550666809082031,14.619333267211914,14.84000015258789,14.731332778930664,14.817333221435547,15.187999725341797,15.047332763671875,14.815333366394043,14.827333450317383,14.620667457580566,14.005999565124512,14.085332870483398,14.063332557678223,14.041333198547363,13.77733325958252,13.480667114257812,13.616666793823242,12.845999717712402,12.791333198547363,12.871333122253418,12.795332908630371,13.104666709899902,13.441332817077637,13.419333457946777,13.770000457763672,13.732000350952148,13.291333198547363,13.680000305175781,13.573332786560059,14.062666893005371,14.557332992553711,14.569999694824219,14.732666969299316,14.490667343139648,14.498666763305664,14.419333457946777,14.186667442321777,13.525333404541016,13.584667205810547,13.623332977294922,13.630666732788086,14.11400032043457,14.473999977111816,13.822667121887207,13.607333183288574,13.583999633789062,13.812666893005371,13.555999755859375,13.155332565307617,13.303999900817871,13.496000289916992,13.375332832336426,12.925333023071289,12.725333213806152,12.687999725341797,12.916000366210938,12.73799991607666,12.578666687011719,13.046667098999023,12.982000350952148,13.380666732788086,13.043333053588867,13.20533275604248,13.308667182922363,13.447999954223633,12.953332901000977,12.694000244140625,12.333333015441895,12.704667091369629,12.584667205810547,12.505999565124512,12.733332633972168,13.539999961853027,13.550000190734863,13.844667434692383,14.005999565124512,14.0600004196167,13.985333442687988,13.830666542053223,13.85533332824707,13.779999732971191,13.78600025177002,13.684666633605957,13.96066665649414,14.629332542419434,14.573332786560059,14.562000274658203,15.436667442321777,15.36533260345459,15.49666690826416,15.069999694824219,15.0686674118042,15.36733341217041,15.529999732971191,15.362000465393066,15.786666870117188,15.77400016784668,15.965999603271484,16.31599998474121,16.211999893188477,16.273332595825195,16.589332580566406,16.583332061767578,16.47599983215332,16.290000915527344,16.374666213989258,16.51533317565918,16.497333526611328,16.495332717895508,16.76333236694336,16.719999313354492,16.6299991607666,16.55666732788086,16.599332809448242,16.39466667175293,16.609333038330078,17.086000442504883,17.066667556762695,16.713333129882812,16.76066780090332,16.71266746520996,16.691999435424805,16.874666213989258,17.360666275024414,17.459333419799805,17.500667572021484,17.319332122802734,17.844667434692383,17.67799949645996,17.91933250427246,17.805999755859375,17.468000411987305,17.884000778198242,17.94333267211914,18.667999267578125,18.648000717163086,17.858667373657227,16.997333526611328,17.19466781616211,17.27666664123535,17.477333068847656,17.709999084472656,17.542667388916016,17.778667449951172,18.310667037963867,18.817333221435547,17.784666061401367,17.857999801635742,17.81333351135254,17.694000244140625,16.867332458496094,17.654666900634766,17.58799934387207,17.785999298095703,17.74333381652832,17.332666397094727,17.75200080871582,18.0086669921875,16.408666610717773,16.167333602905273,16.076000213623047,15.824666976928711,15.878000259399414,16.167333602905273,16.209999084472656,16.999332427978516,17.381332397460938,17.016666412353516,16.14533233642578,15.38466739654541,14.591333389282227,14.66866683959961,14.989333152770996,16.19933319091797,16.565332412719727,16.604000091552734,15.908666610717773,16.512666702270508,16.3713321685791,16.1286678314209,16.544666290283203,16.5939998626709,16.565332412719727,16.682666778564453,16.87933349609375,16.904666900634766,17.483333587646484,17.471332550048828,17.374666213989258,17.613332748413086,17.395999908447266,17.40399932861328,17.541332244873047,17.12733268737793,16.562000274658203,16.44333267211914,16.559999465942383,15.991999626159668,16.504667282104492,16.40999984741211,16.097333908081055,15.46399974822998,15.114666938781738,14.712667465209961,14.371999740600586,14.616666793823242,14.458666801452637,14.753999710083008,15.133999824523926,15.206666946411133,14.20199966430664,14.005999565124512,14.114666938781738,13.939332962036133,14.350666999816895,14.023332595825195,14.197333335876465,14.108667373657227,13.795332908630371,14.252667427062988,13.890000343322754,15.442000389099121,15.451333045959473,15.490667343139648,15.022000312805176,14.433333396911621,14.60533332824707,14.196000099182129,13.812666893005371,14.287332534790039,14.266667366027832,14.73799991607666,14.786666870117188,14.667332649230957,14.516667366027832,14.550000190734863,15.309332847595215,15.440667152404785,15.350666999816895,15.812666893005371,15.465999603271484,15.513999938964844,15.358667373657227,15.408666610717773,15.114666938781738,14.968000411987305,15.137999534606934,14.468000411987305,14.571999549865723,14.739333152770996,15.633999824523926,15.559332847595215,15.36400032043457,15.503999710083008,15.329999923706055,15.313332557678223,15.371333122253418,15.263333320617676,15.812666893005371,15.87266731262207,16.000667572021484,14.894000053405762,14.895333290100098,14.602666854858398,14.376667022705078,14.066666603088379,13.856666564941406,13.998000144958496,13.354000091552734,13.745332717895508,13.666000366210938,13.64799976348877,13.24666690826416,13.33133316040039,13.50333309173584,13.092000007629395,12.904000282287598,12.538000106811523,12.646666526794434,12.74666690826416,13.129332542419434,12.185333251953125,11.565333366394043,11.688667297363281,10.84000015258789,9.866000175476074,9.883333206176758,9.57800006866455,10.031332969665527,10.06933307647705,10.344667434692383,11.245332717895508,11.118000030517578,11.10533332824707,11.849332809448242,11.814000129699707,11.933333396911621,12.495332717895508,12.689332962036133,12.795332908630371,12.423333168029785,12.555999755859375,13.049332618713379,13.402667045593262,13.685999870300293,13.506667137145996,13.914667129516602,13.678667068481445,13.833333015441895,14.34333324432373,14.555999755859375,14.795332908630371,15.092000007629395,15.515999794006348,15.887999534606934,15.616000175476074,14.838666915893555,15.183333396911621,15.350666999816895,15.342000007629395,15.12600040435791,15.317999839782715,15.839332580566406,16.465999603271484,17.031333923339844,17.69466781616211,17.14666748046875,16.67133331298828,16.661333084106445,16.521333694458008,16.968666076660156,16.790666580200195,16.96733283996582,16.92533302307129,16.4913330078125,16.6646671295166,16.55266761779785,16.916667938232422,16.788000106811523,16.916000366210938,16.764667510986328,16.513999938964844,16.05066680908203,16.1200008392334,15.48799991607666,14.837332725524902,14.10200023651123,14.328666687011719,13.928000450134277,13.912667274475098,13.93066692352295,13.8186674118042,13.840666770935059,13.88599967956543,13.644000053405762,14.07800006866455,14.347332954406738,14.685333251953125,14.414667129516602,14.52733325958252,14.638667106628418,15.008000373840332,14.869333267211914,14.881999969482422,14.637332916259766,14.597332954406738,14.599332809448242,14.711999893188477,15.489333152770996,15.701333045959473,15.290666580200195,14.586000442504883,14.524666786193848,14.330666542053223,14.513333320617676,14.528667449951172,14.364666938781738,14.646666526794434,14.640666961669922,13.11066722869873,13.09333324432373,12.876667022705078,13.236666679382324,13.452667236328125,14.012666702270508,14.152000427246094,14.433333396911621,14.26533317565918,14.295999526977539,14.395999908447266,14.45199966430664,14.985333442687988,14.976667404174805,14.835332870483398,14.768667221069336,14.69333267211914,15.083333015441895,15.017333030700684,15.223999977111816,14.699999809265137,14.817999839782715,15.333999633789062,15.300666809082031,15.232666969299316,15.37399959564209,15.652667045593262,15.333999633789062,15.146666526794434,15.052666664123535,15.37399959564209,15.335332870483398,15.077333450317383,15.272000312805176,15.043333053588867,14.994000434875488,15.040666580200195,15.03933334350586,14.907333374023438,14.88266658782959,14.900667190551758,15.0,14.862000465393066,14.989333152770996,14.841333389282227,14.730667114257812,14.666000366210938,14.346667289733887,14.089332580566406,14.133999824523926,13.38466739654541,13.185333251953125,13.522000312805176,13.447333335876465,13.157333374023438,12.964667320251465,13.220000267028809,13.069999694824219,13.093999862670898,13.361332893371582,13.69333267211914,13.755999565124512,13.642666816711426,13.6813325881958,13.76200008392334,13.829999923706055,13.932666778564453,13.720666885375977,13.751333236694336,13.380000114440918,13.60200023651123,14.24666690826416,14.093999862670898,13.897333145141602,13.399999618530273,13.107333183288574,13.396666526794434,13.34000015258789,13.434000015258789,13.349332809448242,13.100666999816895,12.93066692352295,13.273332595825195,13.570667266845703,13.273332595825195,13.339332580566406,13.517333030700684,13.489333152770996,13.482666969299316,13.600666999816895,13.33133316040039,13.182000160217285,12.719332695007324,12.534667015075684,12.494667053222656,12.704000473022461,12.880666732788086,12.996000289916992,12.670666694641113,12.356666564941406,12.570667266845703,12.096667289733887,12.251333236694336,12.26200008392334,12.577333450317383,12.334667205810547,12.3013334274292,12.744667053222656,12.87600040435791,13.109999656677246,13.074666976928711,12.637999534606934,12.626667022705078,12.125332832336426,12.097999572753906,12.453332901000977,12.390000343322754,12.876667022705078,12.81933307647705,12.812000274658203,12.828666687011719,13.210000038146973,13.246000289916992,13.17199993133545,13.499333381652832,13.51533317565918,13.919333457946777,13.846667289733887,13.896666526794434,14.22266674041748,14.635333061218262,14.649333000183105,14.312000274658203,14.246000289916992,14.465999603271484,15.13266658782959,15.116666793823242,15.267333030700684,15.41866683959961,15.324666976928711,15.315333366394043,15.305999755859375,15.850000381469727,15.70533275604248,15.890666961669922,16.250667572021484,16.315332412719727,16.594667434692383,16.974000930786133,16.96466636657715,16.833999633789062,16.863332748413086,16.708667755126953,16.795333862304688,16.615999221801758,16.770000457763672,16.755332946777344,17.184667587280273,17.165332794189453,17.472000122070312,17.946666717529297,17.948667526245117,18.706666946411133,18.73200035095215,18.650667190551758,17.93000030517578,18.148666381835938,18.492666244506836,18.233999252319336,17.06599998474121,17.133333206176758,16.415332794189453,16.666000366210938,16.667999267578125,16.698667526245117,16.771333694458008,16.747333526611328,16.57266616821289,16.45800018310547,16.32666778564453,16.246000289916992,16.411333084106445,17.200000762939453,17.048667907714844,17.469999313354492,17.433332443237305,17.461332321166992,16.711999893188477,17.000667572021484,16.985332489013672,17.54400062561035,18.014667510986328,18.496667861938477,18.492000579833984,18.527999877929688,18.553333282470703,19.90133285522461,20.246667861938477,19.666667938232422,19.913333892822266,20.16933250427246,20.826000213623047,20.58066749572754,19.78933334350586,20.266666412353516,20.09600067138672,20.016666412353516,20.368000030517578,20.167333602905273,20.373332977294922,20.53533363342285,20.91933250427246,20.67799949645996,20.575332641601562,20.937999725341797,21.52199935913086,21.25933265686035,20.73466682434082,19.69733238220215,20.55666732788086,20.479333877563477,21.417333602905273,21.681333541870117,21.540000915527344,21.65399932861328,21.058666229248047,21.134000778198242,20.407333374023438,20.87066650390625,20.722000122070312,20.690000534057617,20.257333755493164,20.681333541870117,21.121999740600586,21.676000595092773,22.34000015258789,22.733999252319336,22.691333770751953,22.656667709350586,23.154666900634766,23.523332595825195,23.976667404174805,24.666667938232422,23.821332931518555,23.93400001525879,25.06333351135254,25.37733268737793,25.022666931152344,24.760000228881836,24.65333366394043,24.81599998474121,25.093332290649414,25.507333755493164,25.56333351135254,25.166000366210938,24.158000946044922,24.749332427978516,24.049999237060547,24.107332229614258,23.507999420166016,21.805999755859375,20.588666915893555,20.881332397460938,21.06999969482422,21.814666748046875,21.968000411987305,21.560667037963867,21.851999282836914,21.30466651916504,21.882667541503906,21.68400001525879,21.994667053222656,21.893333435058594,22.834667205810547,22.639999389648438,22.92333221435547,22.297332763671875,22.33799934387207,21.564666748046875,21.30466651916504,21.72599983215332,23.139333724975586,23.79400062561035,23.67799949645996,24.347999572753906,24.235332489013672,23.69333267211914,23.857999801635742,24.253332138061523,24.155332565307617,24.194000244140625,23.461332321166992,23.163999557495117,22.52400016784668,22.75666618347168,23.51799964904785,23.528667449951172,23.203332901000977,23.04400062561035,23.157333374023438,23.545333862304688,23.726667404174805,23.69333267211914,23.305999755859375,22.968666076660156,23.374000549316406,22.893333435058594,24.246000289916992,24.183332443237305,24.415332794189453,25.176000595092773,25.320667266845703,25.666667938232422,25.00666618347168,24.92733383178711,24.43199920654297,23.4060001373291,22.999332427978516,23.016666412353516,22.731332778930664,22.639999389648438,22.739999771118164,22.768667221069336,23.209333419799805,23.667333602905273,23.68866729736328,23.79199981689453,22.862667083740234,23.70599937438965,23.639999389648438,23.711999893188477,23.704666137695312,23.373332977294922,23.71666717529297,23.976667404174805,23.45400047302246,23.00666618347168,22.468000411987305,22.48933219909668,21.722667694091797,21.744667053222656,21.391332626342773,21.338666915893555,22.101999282836914,21.405332565307617,19.950666427612305,20.4060001373291,20.185333251953125,20.40333366394043,20.292667388916016,20.19933319091797,20.19933319091797,21.02666664123535,20.579999923706055,20.753332138061523,20.833332061767578,21.003332138061523,20.582666397094727,21.187332153320312,20.84000015258789,21.036666870117188,21.12066650390625,21.170000076293945,20.502666473388672,20.59000015258789,20.435333251953125,20.34666633605957,20.246667861938477,20.884000778198242,20.749332427978516,21.0086669921875,21.92733383178711,22.735332489013672,22.601999282836914,22.525999069213867,22.89666748046875,22.591333389282227,22.073333740234375,21.93199920654297,22.110666275024414,21.68000030517578,21.152666091918945,20.775999069213867,21.02400016784668,20.75666618347168,21.368667602539062,21.149999618530273,20.974666595458984,21.10533332824707,22.42733383178711,22.246000289916992,22.31999969482422,22.530000686645508,22.4146671295166,22.67066764831543,23.143999099731445,22.971332550048828,23.334667205810547,23.437332153320312,23.519332885742188,23.05933380126953,22.50933265686035,22.856666564941406,23.302000045776367,23.05466651916504,23.62066650390625,23.28333282470703,22.916667938232422,22.208667755126953,22.264667510986328,23.0,21.01533317565918,20.69466781616211,21.048667907714844,21.577333450317383,21.487333297729492,22.271333694458008,22.365999221801758,22.31800079345703,22.219999313354492,23.077999114990234,23.469999313354492,23.827999114990234,23.39933204650879,22.87066650390625,22.062000274658203,22.341333389282227,22.22333335876465,21.8799991607666,22.15333366394043,21.940000534057617,21.81133270263672,23.034000396728516,22.78933334350586,21.775333404541016,21.706666946411133,21.42333221435547,20.90399932861328,20.703332901000977,21.101999282836914,20.606666564941406,20.1026668548584,20.278667449951172,18.61199951171875,17.185333251953125,17.742000579833984,16.832000732421875,17.8353328704834,19.12933349609375,20.381332397460938,19.953332901000977,19.310667037963867,20.31333351135254,20.062000274658203,19.60533332824707,20.022666931152344,19.413999557495117,19.179332733154297,19.55666732788086,20.005332946777344,19.349332809448242,18.891332626342773,18.8973331451416,18.71266746520996,19.031999588012695,19.60533332824707,19.593332290649414,19.994667053222656,20.07666778564453,18.963333129882812,19.606000900268555,20.184667587280273,20.131332397460938,20.456666946411133,20.334667205810547,20.070667266845703,19.46466636657715,18.94533348083496,19.09866714477539,18.96933364868164,18.454666137695312,18.965999603271484,18.333999633789062,18.60466766357422,18.523332595825195,18.59000015258789,18.917333602905273,19.447999954223633,18.98200035095215,19.454666137695312,19.78266716003418,19.408666610717773,21.299999237060547,21.07266616821289,21.17733383178711,22.139999389648438,22.851333618164062,22.985332489013672,23.847999572753906,23.878000259399414,24.722000122070312,23.503332138061523,24.148000717163086,23.167333602905273,22.242000579833984,22.200666427612305,22.799999237060547,22.96666717529297,23.32866668701172,22.863332748413086,22.33799934387207,20.724000930786133,20.610666275024414,20.593332290649414,21.233999252319336,21.49799919128418,21.263999938964844,21.11400032043457,21.257999420166016,20.67333221435547,21.512666702270508,21.59000015258789,21.34866714477539,20.905332565307617,20.213333129882812,19.82866668701172,20.582666397094727,20.44333267211914,19.812000274658203,19.344667434692383,19.875999450683594,20.055999755859375,23.30266761779785,23.211332321166992,22.799333572387695,25.30466651916504,24.689332962036133,23.496667861938477,23.69933319091797,23.76066780090332,23.176000595092773,22.57933235168457,22.363332748413086,20.366666793823242,20.562667846679688,21.459999084472656,21.44266700744629,21.34000015258789,21.521333694458008,21.284666061401367,20.790666580200195,20.333999633789062,20.209999084472656,20.110666275024414,19.26333236694336,18.715999603271484,18.729999542236328,17.549333572387695,19.03333282470703,18.62933349609375,19.369333267211914,19.297332763671875,19.68000030517578,19.6560001373291,18.997333526611328,19.934667587280273,19.8886661529541,19.940000534057617,19.978666305541992,20.06599998474121,20.6386661529541,20.501333236694336,17.65133285522461,20.713333129882812,20.06800079345703,19.65333366394043,18.788667678833008,17.463333129882812,16.70400047302246,17.520000457763672,17.125333786010742,16.815332412719727,17.25200080871582,17.305999755859375,18.439332962036133,18.118667602539062,17.5939998626709,17.333332061767578,17.39666748046875,19.609333038330078,19.233333587646484,20.99066734313965,22.059999465942383,22.323333740234375,21.99333381652832,22.488000869750977,22.95199966430664,23.0939998626709,22.760000228881836,22.737333297729492,23.21066665649414,23.426666259765625,23.367332458496094,22.0853328704834,22.582000732421875,22.933332443237305,23.229333877563477,23.62066650390625,23.564666748046875,23.166000366210938,22.54599952697754,21.722000122070312,23.066667556762695,22.92799949645996,23.191333770751953,22.744667053222656,23.365333557128906,23.89933204650879,23.979999542236328,24.20400047302246,23.864667892456055,24.343332290649414,24.450666427612305,24.440000534057617,25.119333267211914,24.380666732788086,23.22800064086914,22.468666076660156,22.197999954223633,21.025333404541016,21.31800079345703,19.69266700744629,21.73933219909668,21.075332641601562,22.257999420166016,22.18666648864746,20.674667358398438,20.02400016784668,21.179332733154297,22.33066749572754,22.356666564941406,22.568666458129883,22.99799919128418,23.150667190551758,22.293333053588867,22.961999893188477,23.06999969482422,23.15399932861328,20.150667190551758,19.92799949645996,19.172666549682617,19.43400001525879,19.80266761779785,19.7586669921875,19.83066749572754,20.584667205810547,20.468000411987305,20.81399917602539,20.859333038330078,21.42333221435547,21.148000717163086,20.500667572021484,20.386667251586914,20.856000900268555,20.78733253479004,20.544666290283203,20.251333236694336,20.525333404541016,20.375999450683594,20.17066764831543,19.415332794189453,19.6473331451416,19.917999267578125,19.857332229614258,20.982667922973633,21.325332641601562,19.652666091918945,19.02400016784668,18.43600082397461,18.416000366210938,18.439332962036133,18.94266700744629,19.39466667175293,18.890666961669922,19.263999938964844,19.33066749572754,18.36199951171875,17.965999603271484,17.83133316040039,18.239999771118164,18.26799964904785,17.635332107543945,17.3613338470459,17.851333618164062,18.32200050354004,18.57466697692871,18.657333374023438,19.278667449951172,19.058666229248047,19.45400047302246,17.851999282836914,18.33066749572754,18.213333129882812,18.15399932861328,18.40399932861328,17.89466667175293,17.84666633605957,17.7586669921875,18.224000930786133,18.082000732421875,18.21733283996582,17.516666412353516,17.593332290649414,17.243999481201172,16.5086669921875,15.675999641418457,16.097999572753906,15.912667274475098,15.600666999816895,16.273332595825195,17.00200080871582,17.022666931152344,16.470666885375977,16.32266616821289,16.131999969482422,15.968000411987305,15.133999824523926,15.487333297729492,15.463333129882812,15.222000122070312,14.0686674118042,13.690667152404785,13.67199993133545,12.84866714477539,13.03266716003418,12.708666801452637,12.579999923706055,12.657333374023438,12.54800033569336,12.343999862670898,11.9313325881958,12.90666675567627,13.105999946594238,13.729999542236328,13.633333206176758,14.192000389099121,14.473333358764648,13.950667381286621,14.260666847229004,14.32800006866455,15.001999855041504,14.982666969299316,15.095333099365234,14.641332626342773,14.790666580200195,14.909333229064941,14.650667190551758,14.618000030517578,14.855999946594238,14.897333145141602,15.14466667175293,14.970000267028809,15.65999984741211,15.539999961853027,15.355999946594238,15.337332725524902,15.928000450134277,15.90666675567627,16.338666915893555,16.899999618530273,16.825332641601562,16.99066734313965,16.902666091918945,17.211999893188477,17.045333862304688,17.344667434692383,17.658666610717773,15.254667282104492,15.202667236328125,15.718000411987305,16.150667190551758,16.107332229614258,15.59000015258789,15.62266731262207,15.221332550048828,15.383333206176758,15.561332702636719,15.886667251586914,15.667332649230957,15.267333030700684,15.666666984558105,14.641332626342773,14.37600040435791,14.662667274475098,15.121999740600586,15.057332992553711,14.722000122070312,14.8100004196167,14.09333324432373,14.333333015441895,14.272000312805176,14.37266731262207,14.780667304992676,15.040666580200195,15.000666618347168,14.711999893188477,15.305333137512207,15.16333293914795,15.452667236328125,15.702667236328125,16.47333335876465,16.391332626342773,16.34666633605957,16.187332153320312,16.319332122802734,16.232667922973633,16.440000534057617,16.041332244873047,16.082000732421875,14.880666732788086,15.24666690826416,16.17066764831543,16.142000198364258,16.058000564575195,16.312667846679688,16.208667755126953,15.535332679748535,15.428667068481445,15.847999572753906,16.003332138061523,16.302000045776367,16.31599998474121,16.525999069213867,17.130666732788086,17.19266700744629,17.316667556762695,17.46466636657715,17.1299991607666,16.899999618530273,17.038667678833008,16.978666305541992,19.978666305541992,21.875333786010742,21.847333908081055,21.08133316040039,21.000667572021484,20.994667053222656,20.887332916259766,21.1646671295166,21.148000717163086,21.77199935913086,22.369333267211914,22.47599983215332,23.006000518798828,23.32866668701172,23.073999404907227,23.290000915527344,23.47800064086914,23.332666397094727,23.968000411987305,23.481332778930664,23.655332565307617,22.202667236328125,22.422666549682617,21.92799949645996,22.086000442504883,21.996000289916992,22.32466697692871,22.413333892822266,22.20199966430664,22.024667739868164,22.392667770385742,22.635332107543945,23.256000518798828,23.51333236694336,23.978666305541992,23.892667770385742,25.433332443237305,25.266000747680664,26.209999084472656,26.93600082397461,27.03933334350586,27.947999954223633,28.350000381469727,28.729333877563477,28.691999435424805,27.64666748046875,27.8886661529541,28.68400001525879,29.534000396728516,30.1026668548584,31.270666122436523,32.80933380126953,32.089332580566406,31.876667022705078,34.990665435791016,35.861331939697266,34.56666564941406,34.232666015625,34.03333282470703,36.47999954223633,37.97066879272461,38.14666748046875,37.654666900634766,37.201332092285156,37.793331146240234,38.732666015625,42.72066879272461,43.371334075927734,52.0,59.137332916259766,48.97999954223633,49.930667877197266,49.871334075927734,51.41866683959961,51.62533187866211,51.15266799926758,53.599998474121094,53.33533477783203,57.22666549682617,61.16133117675781,59.96066665649414,60.06666564941406,55.58599853515625,53.32733154296875,51.91999816894531,45.266666412353516,44.53266525268555,49.574668884277344,49.70066833496094,49.96666717529297,48.30266571044922,46.89866638183594,40.53333282470703,43.02199935913086,42.28200149536133,37.369998931884766,36.44133377075195,29.67133331298828,28.68000030517578,24.08133316040039,28.50933265686035,28.50200080871582,28.952667236328125,33.66666793823242,35.95000076293945,35.21066665649414,34.29066848754883,33.47533416748047,34.93333435058594,32.104000091552734,30.29800033569336,32.000667572021484,34.41600036621094,36.36333465576172,36.589332580566406,38.20000076293945,43.39666748046875,47.32600021362305,48.65533447265625,49.680667877197266,50.259334564208984,49.75733184814453,45.781333923339844,48.807334899902344,47.04199981689453,48.34333419799805,53.25,51.27466583251953,53.367332458496094,52.12533187866211,46.75466537475586,50.74599838256836,51.2140007019043,52.172000885009766,52.00266647338867,54.62799835205078,54.08599853515625,53.96066665649414,52.73066711425781,53.55533218383789,53.27799987792969,54.242000579833984,53.867332458496094,54.37066650390625,55.17333221435547,54.45866775512695,54.591331481933594,54.68199920654297,53.72066879272461,55.66666793823242,59.87333297729492,58.770668029785156,58.86399841308594,57.62533187866211,59.04399871826172,63.327999114990234,62.711334228515625,68.336669921875,64.85600280761719,62.35200119018555,66.05999755859375,65.47533416748047,66.11933135986328,66.9306640625,66.72666931152344,66.28800201416016,66.78533172607422,64.0566635131836,65.73200225830078,63.982666015625,67.29000091552734,71.98733520507812,74.64199829101562,80.57733154296875,91.43866729736328,92.65733337402344,91.05867004394531,92.9520034790039,102.97666931152344,99.80400085449219,101.12000274658203,103.06732940673828,100.04266357421875,100.05599975585938,109.53333282470703,104.55733489990234,106.15533447265625,100.87133026123047,94.46666717529297,102.63999938964844,98.43267059326172,99.94066619873047,99.16600036621094,95.38400268554688,99.0,99.13333129882812,99.00133514404297,99.30533599853516,96.84733581542969,94.57133483886719,91.6259994506836,103.65066528320312,108.06666564941406,110.04733276367188,122.3759994506836,125.80599975585938,125.23533630371094,133.45533752441406,136.6653289794922,134.27999877929688,134.8893280029297,143.54466247558594,149.25,147.55999755859375,166.10667419433594,158.35000610351562,149.1233367919922,135.6666717529297,139.44000244140625,110.06999969482422,122.09333038330078,123.77999877929688,124.23999786376953,139.8733367919922,149.9199981689453,147.25332641601562,141.14332580566406,147.38333129882812,149.79666137695312,141.41000366210938,126.78666687011719,129.26333618164062,135.77999877929688,140.39999389648438,139.69000244140625,143.00332641601562,149.3866729736328,138.3633270263672,141.89332580566406,137.9933319091797,141.76666259765625,141.97332763671875,144.6666717529297,147.43333435058594,148.88333129882812,153.76666259765625,149.6266632080078,146.55667114257812,143.61000061035156,140.64666748046875,140.8800048828125,141.92999267578125,140.2100067138672,140.0933380126953,141.55999755859375,135.33999633789062,136.94332885742188,129.34666442871094,133.50332641601562,141.3000030517578,140.32666015625,146.02999877929688,143.31666564941406,140.4199981689453,136.7866668701172,139.0433349609375,137.25332641601562,136.1666717529297,136.02999877929688,147.20333862304688,162.2133331298828,166.42333984375,163.20333862304688,173.9499969482422,185.1266632080078,191.3333282470703,195.25332641601562,189.1999969482422,194.9199981689453,189.60667419433594,197.7933349609375,199.67999267578125,213.9199981689453,216.6266632080078,201.4933319091797,209.02333068847656,203.3300018310547,213.27667236328125,211.0833282470703,207.58999633789062,218.63333129882812,231.6666717529297,216.6199951171875,213.44667053222656,215.32666015625,220.58999633789062,221.22999572753906,221.99667358398438,231.5933380126953,235.22332763671875,243.2566680908203,245.0366668701172,251.9933319091797,272.0133361816406,293.3399963378906,270.39666748046875,283.14666748046875,284.8033447265625,281.6666564941406,275.38665771484375,281.51666259765625,283.48333740234375,281.663330078125,282.21331787109375,293.6000061035156,294.36334228515625,288.0533447265625,278.4766540527344,264.510009765625,279.9366760253906,290.92999267578125,284.89666748046875,283.3299865722656,284.07666015625,287.8066711425781,283.1533203125,268.2733459472656,270.5533447265625,272.0400085449219,265.40667724609375,266.04998779296875,262.4599914550781,260.4333190917969,238.1666717529297,232.94667053222656,247.33999633789062,227.4066619873047,225.1666717529297,239.47666931152344,228.81333923339844,217.73333740234375,207.14666748046875,199.31666564941406,187.6666717529297,224.52667236328125,222.68666076660156,233.1999969482422,231.2433319091797,235.97999572753906,225.6266632080078,233.93666076660156,217.72000122070312,218.2899932861328,223.3333282470703,220.72000122070312,210.08999633789062,213.4633331298828,206.23666381835938,203.76333618164062,211.8733367919922,222.64332580566406,220.5833282470703,230.35000610351562,230.5399932861328,223.6566619873047,227.93333435058594,225.67333984375,233.9933319091797,254.10667419433594,244.07666015625,246.28334045410156,246.5933380126953,238.2100067138672,239.663330078125,248.0399932861328,239.89666748046875,243.13333129882812,246.06666564941406,234.913330078125,231.46665954589844,225.6666717529297,236.47999572753906,228.3000030517578,224.53334045410156,223.64666748046875,221.17999267578125,224.1233367919922,209.67999267578125,205.73333740234375,196.6300048828125,190.56333923339844,196.5800018310547,192.27667236328125,192.6233367919922,187.82000732421875,195.5933380126953,193.6266632080078,202.14666748046875,201.56333923339844,206.3766632080078,210.28334045410156,208.4066619873047,207.96665954589844,201.7066650390625,190.94667053222656,199.68333435058594,201.7100067138672,201.19667053222656,199.5933380126953,203.3733367919922,203.29666137695312,205.89666748046875],"type":"scatter","xaxis":"x","yaxis":"y"},{"name":"Revenue","x":["2021-01-01T00:00:00","2020-01-01T00:00:00","2019-01-01T00:00:00","2018-01-01T00:00:00","2017-01-01T00:00:00","2016-01-01T00:00:00","2015-01-01T00:00:00","2014-01-01T00:00:00","2013-01-01T00:00:00","2012-01-01T00:00:00","2011-01-01T00:00:00","2010-01-01T00:00:00","2009-01-01T00:00:00"],"y":[53823.0,31536.0,24578.0,21461.0,11759.0,7000.0,4046.0,3198.0,2013.0,413.0,204.0,117.0,112.0],"type":"scatter","xaxis":"x2","yaxis":"y2"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"matches":"x2","showticklabels":false,"title":{"text":"Date"},"rangeslider":{"visible":true}},"yaxis":{"anchor":"x","domain":[0.6499999999999999,0.9999999999999999],"title":{"text":"Price ($US)"}},"xaxis2":{"anchor":"y2","domain":[0.0,1.0],"title":{"text":"Date"}},"yaxis2":{"anchor":"x2","domain":[0.0,0.35],"title":{"text":"Revenue ($US Millions)"}},"annotations":[{"font":{"size":16},"showarrow":false,"text":"Historical Share Price","x":0.5,"xanchor":"center","xref":"paper","y":0.9999999999999999,"yanchor":"bottom","yref":"paper"},{"font":{"size":16},"showarrow":false,"text":"Historical Revenue","x":0.5,"xanchor":"center","xref":"paper","y":0.35,"yanchor":"bottom","yref":"paper"}],"showlegend":false,"height":900,"title":{"text":"Tesla"}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('1984855c-8134-4daf-8421-857f0cdd4c99');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


## Question 6: Plot GameStop Stock Graph


Use the `make_graph` function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`. Note the graph will only show data upto June 2021.



```python
make_graph(gme_data, gme_revenue, 'GameStop')
```


<div>                            <div id="359c44ce-308d-462b-9035-f806c3eb99ff" class="plotly-graph-div" style="height:900px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("359c44ce-308d-462b-9035-f806c3eb99ff")) {                    Plotly.newPlot(                        "359c44ce-308d-462b-9035-f806c3eb99ff",                        [{"name":"Share Price","x":["2002-02-13T00:00:00","2002-02-14T00:00:00","2002-02-15T00:00:00","2002-02-19T00:00:00","2002-02-20T00:00:00","2002-02-21T00:00:00","2002-02-22T00:00:00","2002-02-25T00:00:00","2002-02-26T00:00:00","2002-02-27T00:00:00","2002-02-28T00:00:00","2002-03-01T00:00:00","2002-03-04T00:00:00","2002-03-05T00:00:00","2002-03-06T00:00:00","2002-03-07T00:00:00","2002-03-08T00:00:00","2002-03-11T00:00:00","2002-03-12T00:00:00","2002-03-13T00:00:00","2002-03-14T00:00:00","2002-03-15T00:00:00","2002-03-18T00:00:00","2002-03-19T00:00:00","2002-03-20T00:00:00","2002-03-21T00:00:00","2002-03-22T00:00:00","2002-03-25T00:00:00","2002-03-26T00:00:00","2002-03-27T00:00:00","2002-03-28T00:00:00","2002-04-01T00:00:00","2002-04-02T00:00:00","2002-04-03T00:00:00","2002-04-04T00:00:00","2002-04-05T00:00:00","2002-04-08T00:00:00","2002-04-09T00:00:00","2002-04-10T00:00:00","2002-04-11T00:00:00","2002-04-12T00:00:00","2002-04-15T00:00:00","2002-04-16T00:00:00","2002-04-17T00:00:00","2002-04-18T00:00:00","2002-04-19T00:00:00","2002-04-22T00:00:00","2002-04-23T00:00:00","2002-04-24T00:00:00","2002-04-25T00:00:00","2002-04-26T00:00:00","2002-04-29T00:00:00","2002-04-30T00:00:00","2002-05-01T00:00:00","2002-05-02T00:00:00","2002-05-03T00:00:00","2002-05-06T00:00:00","2002-05-07T00:00:00","2002-05-08T00:00:00","2002-05-09T00:00:00","2002-05-10T00:00:00","2002-05-13T00:00:00","2002-05-14T00:00:00","2002-05-15T00:00:00","2002-05-16T00:00:00","2002-05-17T00:00:00","2002-05-20T00:00:00","2002-05-21T00:00:00","2002-05-22T00:00:00","2002-05-23T00:00:00","2002-05-24T00:00:00","2002-05-28T00:00:00","2002-05-29T00:00:00","2002-05-30T00:00:00","2002-05-31T00:00:00","2002-06-03T00:00:00","2002-06-04T00:00:00","2002-06-05T00:00:00","2002-06-06T00:00:00","2002-06-07T00:00:00","2002-06-10T00:00:00","2002-06-11T00:00:00","2002-06-12T00:00:00","2002-06-13T00:00:00","2002-06-14T00:00:00","2002-06-17T00:00:00","2002-06-18T00:00:00","2002-06-19T00:00:00","2002-06-20T00:00:00","2002-06-21T00:00:00","2002-06-24T00:00:00","2002-06-25T00:00:00","2002-06-26T00:00:00","2002-06-27T00:00:00","2002-06-28T00:00:00","2002-07-01T00:00:00","2002-07-02T00:00:00","2002-07-03T00:00:00","2002-07-05T00:00:00","2002-07-08T00:00:00","2002-07-09T00:00:00","2002-07-10T00:00:00","2002-07-11T00:00:00","2002-07-12T00:00:00","2002-07-15T00:00:00","2002-07-16T00:00:00","2002-07-17T00:00:00","2002-07-18T00:00:00","2002-07-19T00:00:00","2002-07-22T00:00:00","2002-07-23T00:00:00","2002-07-24T00:00:00","2002-07-25T00:00:00","2002-07-26T00:00:00","2002-07-29T00:00:00","2002-07-30T00:00:00","2002-07-31T00:00:00","2002-08-01T00:00:00","2002-08-02T00:00:00","2002-08-05T00:00:00","2002-08-06T00:00:00","2002-08-07T00:00:00","2002-08-08T00:00:00","2002-08-09T00:00:00","2002-08-12T00:00:00","2002-08-13T00:00:00","2002-08-14T00:00:00","2002-08-15T00:00:00","2002-08-16T00:00:00","2002-08-19T00:00:00","2002-08-20T00:00:00","2002-08-21T00:00:00","2002-08-22T00:00:00","2002-08-23T00:00:00","2002-08-26T00:00:00","2002-08-27T00:00:00","2002-08-28T00:00:00","2002-08-29T00:00:00","2002-08-30T00:00:00","2002-09-03T00:00:00","2002-09-04T00:00:00","2002-09-05T00:00:00","2002-09-06T00:00:00","2002-09-09T00:00:00","2002-09-10T00:00:00","2002-09-11T00:00:00","2002-09-12T00:00:00","2002-09-13T00:00:00","2002-09-16T00:00:00","2002-09-17T00:00:00","2002-09-18T00:00:00","2002-09-19T00:00:00","2002-09-20T00:00:00","2002-09-23T00:00:00","2002-09-24T00:00:00","2002-09-25T00:00:00","2002-09-26T00:00:00","2002-09-27T00:00:00","2002-09-30T00:00:00","2002-10-01T00:00:00","2002-10-02T00:00:00","2002-10-03T00:00:00","2002-10-04T00:00:00","2002-10-07T00:00:00","2002-10-08T00:00:00","2002-10-09T00:00:00","2002-10-10T00:00:00","2002-10-11T00:00:00","2002-10-14T00:00:00","2002-10-15T00:00:00","2002-10-16T00:00:00","2002-10-17T00:00:00","2002-10-18T00:00:00","2002-10-21T00:00:00","2002-10-22T00:00:00","2002-10-23T00:00:00","2002-10-24T00:00:00","2002-10-25T00:00:00","2002-10-28T00:00:00","2002-10-29T00:00:00","2002-10-30T00:00:00","2002-10-31T00:00:00","2002-11-01T00:00:00","2002-11-04T00:00:00","2002-11-05T00:00:00","2002-11-06T00:00:00","2002-11-07T00:00:00","2002-11-08T00:00:00","2002-11-11T00:00:00","2002-11-12T00:00:00","2002-11-13T00:00:00","2002-11-14T00:00:00","2002-11-15T00:00:00","2002-11-18T00:00:00","2002-11-19T00:00:00","2002-11-20T00:00:00","2002-11-21T00:00:00","2002-11-22T00:00:00","2002-11-25T00:00:00","2002-11-26T00:00:00","2002-11-27T00:00:00","2002-11-29T00:00:00","2002-12-02T00:00:00","2002-12-03T00:00:00","2002-12-04T00:00:00","2002-12-05T00:00:00","2002-12-06T00:00:00","2002-12-09T00:00:00","2002-12-10T00:00:00","2002-12-11T00:00:00","2002-12-12T00:00:00","2002-12-13T00:00:00","2002-12-16T00:00:00","2002-12-17T00:00:00","2002-12-18T00:00:00","2002-12-19T00:00:00","2002-12-20T00:00:00","2002-12-23T00:00:00","2002-12-24T00:00:00","2002-12-26T00:00:00","2002-12-27T00:00:00","2002-12-30T00:00:00","2002-12-31T00:00:00","2003-01-02T00:00:00","2003-01-03T00:00:00","2003-01-06T00:00:00","2003-01-07T00:00:00","2003-01-08T00:00:00","2003-01-09T00:00:00","2003-01-10T00:00:00","2003-01-13T00:00:00","2003-01-14T00:00:00","2003-01-15T00:00:00","2003-01-16T00:00:00","2003-01-17T00:00:00","2003-01-21T00:00:00","2003-01-22T00:00:00","2003-01-23T00:00:00","2003-01-24T00:00:00","2003-01-27T00:00:00","2003-01-28T00:00:00","2003-01-29T00:00:00","2003-01-30T00:00:00","2003-01-31T00:00:00","2003-02-03T00:00:00","2003-02-04T00:00:00","2003-02-05T00:00:00","2003-02-06T00:00:00","2003-02-07T00:00:00","2003-02-10T00:00:00","2003-02-11T00:00:00","2003-02-12T00:00:00","2003-02-13T00:00:00","2003-02-14T00:00:00","2003-02-18T00:00:00","2003-02-19T00:00:00","2003-02-20T00:00:00","2003-02-21T00:00:00","2003-02-24T00:00:00","2003-02-25T00:00:00","2003-02-26T00:00:00","2003-02-27T00:00:00","2003-02-28T00:00:00","2003-03-03T00:00:00","2003-03-04T00:00:00","2003-03-05T00:00:00","2003-03-06T00:00:00","2003-03-07T00:00:00","2003-03-10T00:00:00","2003-03-11T00:00:00","2003-03-12T00:00:00","2003-03-13T00:00:00","2003-03-14T00:00:00","2003-03-17T00:00:00","2003-03-18T00:00:00","2003-03-19T00:00:00","2003-03-20T00:00:00","2003-03-21T00:00:00","2003-03-24T00:00:00","2003-03-25T00:00:00","2003-03-26T00:00:00","2003-03-27T00:00:00","2003-03-28T00:00:00","2003-03-31T00:00:00","2003-04-01T00:00:00","2003-04-02T00:00:00","2003-04-03T00:00:00","2003-04-04T00:00:00","2003-04-07T00:00:00","2003-04-08T00:00:00","2003-04-09T00:00:00","2003-04-10T00:00:00","2003-04-11T00:00:00","2003-04-14T00:00:00","2003-04-15T00:00:00","2003-04-16T00:00:00","2003-04-17T00:00:00","2003-04-21T00:00:00","2003-04-22T00:00:00","2003-04-23T00:00:00","2003-04-24T00:00:00","2003-04-25T00:00:00","2003-04-28T00:00:00","2003-04-29T00:00:00","2003-04-30T00:00:00","2003-05-01T00:00:00","2003-05-02T00:00:00","2003-05-05T00:00:00","2003-05-06T00:00:00","2003-05-07T00:00:00","2003-05-08T00:00:00","2003-05-09T00:00:00","2003-05-12T00:00:00","2003-05-13T00:00:00","2003-05-14T00:00:00","2003-05-15T00:00:00","2003-05-16T00:00:00","2003-05-19T00:00:00","2003-05-20T00:00:00","2003-05-21T00:00:00","2003-05-22T00:00:00","2003-05-23T00:00:00","2003-05-27T00:00:00","2003-05-28T00:00:00","2003-05-29T00:00:00","2003-05-30T00:00:00","2003-06-02T00:00:00","2003-06-03T00:00:00","2003-06-04T00:00:00","2003-06-05T00:00:00","2003-06-06T00:00:00","2003-06-09T00:00:00","2003-06-10T00:00:00","2003-06-11T00:00:00","2003-06-12T00:00:00","2003-06-13T00:00:00","2003-06-16T00:00:00","2003-06-17T00:00:00","2003-06-18T00:00:00","2003-06-19T00:00:00","2003-06-20T00:00:00","2003-06-23T00:00:00","2003-06-24T00:00:00","2003-06-25T00:00:00","2003-06-26T00:00:00","2003-06-27T00:00:00","2003-06-30T00:00:00","2003-07-01T00:00:00","2003-07-02T00:00:00","2003-07-03T00:00:00","2003-07-07T00:00:00","2003-07-08T00:00:00","2003-07-09T00:00:00","2003-07-10T00:00:00","2003-07-11T00:00:00","2003-07-14T00:00:00","2003-07-15T00:00:00","2003-07-16T00:00:00","2003-07-17T00:00:00","2003-07-18T00:00:00","2003-07-21T00:00:00","2003-07-22T00:00:00","2003-07-23T00:00:00","2003-07-24T00:00:00","2003-07-25T00:00:00","2003-07-28T00:00:00","2003-07-29T00:00:00","2003-07-30T00:00:00","2003-07-31T00:00:00","2003-08-01T00:00:00","2003-08-04T00:00:00","2003-08-05T00:00:00","2003-08-06T00:00:00","2003-08-07T00:00:00","2003-08-08T00:00:00","2003-08-11T00:00:00","2003-08-12T00:00:00","2003-08-13T00:00:00","2003-08-14T00:00:00","2003-08-15T00:00:00","2003-08-18T00:00:00","2003-08-19T00:00:00","2003-08-20T00:00:00","2003-08-21T00:00:00","2003-08-22T00:00:00","2003-08-25T00:00:00","2003-08-26T00:00:00","2003-08-27T00:00:00","2003-08-28T00:00:00","2003-08-29T00:00:00","2003-09-02T00:00:00","2003-09-03T00:00:00","2003-09-04T00:00:00","2003-09-05T00:00:00","2003-09-08T00:00:00","2003-09-09T00:00:00","2003-09-10T00:00:00","2003-09-11T00:00:00","2003-09-12T00:00:00","2003-09-15T00:00:00","2003-09-16T00:00:00","2003-09-17T00:00:00","2003-09-18T00:00:00","2003-09-19T00:00:00","2003-09-22T00:00:00","2003-09-23T00:00:00","2003-09-24T00:00:00","2003-09-25T00:00:00","2003-09-26T00:00:00","2003-09-29T00:00:00","2003-09-30T00:00:00","2003-10-01T00:00:00","2003-10-02T00:00:00","2003-10-03T00:00:00","2003-10-06T00:00:00","2003-10-07T00:00:00","2003-10-08T00:00:00","2003-10-09T00:00:00","2003-10-10T00:00:00","2003-10-13T00:00:00","2003-10-14T00:00:00","2003-10-15T00:00:00","2003-10-16T00:00:00","2003-10-17T00:00:00","2003-10-20T00:00:00","2003-10-21T00:00:00","2003-10-22T00:00:00","2003-10-23T00:00:00","2003-10-24T00:00:00","2003-10-27T00:00:00","2003-10-28T00:00:00","2003-10-29T00:00:00","2003-10-30T00:00:00","2003-10-31T00:00:00","2003-11-03T00:00:00","2003-11-04T00:00:00","2003-11-05T00:00:00","2003-11-06T00:00:00","2003-11-07T00:00:00","2003-11-10T00:00:00","2003-11-11T00:00:00","2003-11-12T00:00:00","2003-11-13T00:00:00","2003-11-14T00:00:00","2003-11-17T00:00:00","2003-11-18T00:00:00","2003-11-19T00:00:00","2003-11-20T00:00:00","2003-11-21T00:00:00","2003-11-24T00:00:00","2003-11-25T00:00:00","2003-11-26T00:00:00","2003-11-28T00:00:00","2003-12-01T00:00:00","2003-12-02T00:00:00","2003-12-03T00:00:00","2003-12-04T00:00:00","2003-12-05T00:00:00","2003-12-08T00:00:00","2003-12-09T00:00:00","2003-12-10T00:00:00","2003-12-11T00:00:00","2003-12-12T00:00:00","2003-12-15T00:00:00","2003-12-16T00:00:00","2003-12-17T00:00:00","2003-12-18T00:00:00","2003-12-19T00:00:00","2003-12-22T00:00:00","2003-12-23T00:00:00","2003-12-24T00:00:00","2003-12-26T00:00:00","2003-12-29T00:00:00","2003-12-30T00:00:00","2003-12-31T00:00:00","2004-01-02T00:00:00","2004-01-05T00:00:00","2004-01-06T00:00:00","2004-01-07T00:00:00","2004-01-08T00:00:00","2004-01-09T00:00:00","2004-01-12T00:00:00","2004-01-13T00:00:00","2004-01-14T00:00:00","2004-01-15T00:00:00","2004-01-16T00:00:00","2004-01-20T00:00:00","2004-01-21T00:00:00","2004-01-22T00:00:00","2004-01-23T00:00:00","2004-01-26T00:00:00","2004-01-27T00:00:00","2004-01-28T00:00:00","2004-01-29T00:00:00","2004-01-30T00:00:00","2004-02-02T00:00:00","2004-02-03T00:00:00","2004-02-04T00:00:00","2004-02-05T00:00:00","2004-02-06T00:00:00","2004-02-09T00:00:00","2004-02-10T00:00:00","2004-02-11T00:00:00","2004-02-12T00:00:00","2004-02-13T00:00:00","2004-02-17T00:00:00","2004-02-18T00:00:00","2004-02-19T00:00:00","2004-02-20T00:00:00","2004-02-23T00:00:00","2004-02-24T00:00:00","2004-02-25T00:00:00","2004-02-26T00:00:00","2004-02-27T00:00:00","2004-03-01T00:00:00","2004-03-02T00:00:00","2004-03-03T00:00:00","2004-03-04T00:00:00","2004-03-05T00:00:00","2004-03-08T00:00:00","2004-03-09T00:00:00","2004-03-10T00:00:00","2004-03-11T00:00:00","2004-03-12T00:00:00","2004-03-15T00:00:00","2004-03-16T00:00:00","2004-03-17T00:00:00","2004-03-18T00:00:00","2004-03-19T00:00:00","2004-03-22T00:00:00","2004-03-23T00:00:00","2004-03-24T00:00:00","2004-03-25T00:00:00","2004-03-26T00:00:00","2004-03-29T00:00:00","2004-03-30T00:00:00","2004-03-31T00:00:00","2004-04-01T00:00:00","2004-04-02T00:00:00","2004-04-05T00:00:00","2004-04-06T00:00:00","2004-04-07T00:00:00","2004-04-08T00:00:00","2004-04-12T00:00:00","2004-04-13T00:00:00","2004-04-14T00:00:00","2004-04-15T00:00:00","2004-04-16T00:00:00","2004-04-19T00:00:00","2004-04-20T00:00:00","2004-04-21T00:00:00","2004-04-22T00:00:00","2004-04-23T00:00:00","2004-04-26T00:00:00","2004-04-27T00:00:00","2004-04-28T00:00:00","2004-04-29T00:00:00","2004-04-30T00:00:00","2004-05-03T00:00:00","2004-05-04T00:00:00","2004-05-05T00:00:00","2004-05-06T00:00:00","2004-05-07T00:00:00","2004-05-10T00:00:00","2004-05-11T00:00:00","2004-05-12T00:00:00","2004-05-13T00:00:00","2004-05-14T00:00:00","2004-05-17T00:00:00","2004-05-18T00:00:00","2004-05-19T00:00:00","2004-05-20T00:00:00","2004-05-21T00:00:00","2004-05-24T00:00:00","2004-05-25T00:00:00","2004-05-26T00:00:00","2004-05-27T00:00:00","2004-05-28T00:00:00","2004-06-01T00:00:00","2004-06-02T00:00:00","2004-06-03T00:00:00","2004-06-04T00:00:00","2004-06-07T00:00:00","2004-06-08T00:00:00","2004-06-09T00:00:00","2004-06-10T00:00:00","2004-06-14T00:00:00","2004-06-15T00:00:00","2004-06-16T00:00:00","2004-06-17T00:00:00","2004-06-18T00:00:00","2004-06-21T00:00:00","2004-06-22T00:00:00","2004-06-23T00:00:00","2004-06-24T00:00:00","2004-06-25T00:00:00","2004-06-28T00:00:00","2004-06-29T00:00:00","2004-06-30T00:00:00","2004-07-01T00:00:00","2004-07-02T00:00:00","2004-07-06T00:00:00","2004-07-07T00:00:00","2004-07-08T00:00:00","2004-07-09T00:00:00","2004-07-12T00:00:00","2004-07-13T00:00:00","2004-07-14T00:00:00","2004-07-15T00:00:00","2004-07-16T00:00:00","2004-07-19T00:00:00","2004-07-20T00:00:00","2004-07-21T00:00:00","2004-07-22T00:00:00","2004-07-23T00:00:00","2004-07-26T00:00:00","2004-07-27T00:00:00","2004-07-28T00:00:00","2004-07-29T00:00:00","2004-07-30T00:00:00","2004-08-02T00:00:00","2004-08-03T00:00:00","2004-08-04T00:00:00","2004-08-05T00:00:00","2004-08-06T00:00:00","2004-08-09T00:00:00","2004-08-10T00:00:00","2004-08-11T00:00:00","2004-08-12T00:00:00","2004-08-13T00:00:00","2004-08-16T00:00:00","2004-08-17T00:00:00","2004-08-18T00:00:00","2004-08-19T00:00:00","2004-08-20T00:00:00","2004-08-23T00:00:00","2004-08-24T00:00:00","2004-08-25T00:00:00","2004-08-26T00:00:00","2004-08-27T00:00:00","2004-08-30T00:00:00","2004-08-31T00:00:00","2004-09-01T00:00:00","2004-09-02T00:00:00","2004-09-03T00:00:00","2004-09-07T00:00:00","2004-09-08T00:00:00","2004-09-09T00:00:00","2004-09-10T00:00:00","2004-09-13T00:00:00","2004-09-14T00:00:00","2004-09-15T00:00:00","2004-09-16T00:00:00","2004-09-17T00:00:00","2004-09-20T00:00:00","2004-09-21T00:00:00","2004-09-22T00:00:00","2004-09-23T00:00:00","2004-09-24T00:00:00","2004-09-27T00:00:00","2004-09-28T00:00:00","2004-09-29T00:00:00","2004-09-30T00:00:00","2004-10-01T00:00:00","2004-10-04T00:00:00","2004-10-05T00:00:00","2004-10-06T00:00:00","2004-10-07T00:00:00","2004-10-08T00:00:00","2004-10-11T00:00:00","2004-10-12T00:00:00","2004-10-13T00:00:00","2004-10-14T00:00:00","2004-10-15T00:00:00","2004-10-18T00:00:00","2004-10-19T00:00:00","2004-10-20T00:00:00","2004-10-21T00:00:00","2004-10-22T00:00:00","2004-10-25T00:00:00","2004-10-26T00:00:00","2004-10-27T00:00:00","2004-10-28T00:00:00","2004-10-29T00:00:00","2004-11-01T00:00:00","2004-11-02T00:00:00","2004-11-03T00:00:00","2004-11-04T00:00:00","2004-11-05T00:00:00","2004-11-08T00:00:00","2004-11-09T00:00:00","2004-11-10T00:00:00","2004-11-11T00:00:00","2004-11-12T00:00:00","2004-11-15T00:00:00","2004-11-16T00:00:00","2004-11-17T00:00:00","2004-11-18T00:00:00","2004-11-19T00:00:00","2004-11-22T00:00:00","2004-11-23T00:00:00","2004-11-24T00:00:00","2004-11-26T00:00:00","2004-11-29T00:00:00","2004-11-30T00:00:00","2004-12-01T00:00:00","2004-12-02T00:00:00","2004-12-03T00:00:00","2004-12-06T00:00:00","2004-12-07T00:00:00","2004-12-08T00:00:00","2004-12-09T00:00:00","2004-12-10T00:00:00","2004-12-13T00:00:00","2004-12-14T00:00:00","2004-12-15T00:00:00","2004-12-16T00:00:00","2004-12-17T00:00:00","2004-12-20T00:00:00","2004-12-21T00:00:00","2004-12-22T00:00:00","2004-12-23T00:00:00","2004-12-27T00:00:00","2004-12-28T00:00:00","2004-12-29T00:00:00","2004-12-30T00:00:00","2004-12-31T00:00:00","2005-01-03T00:00:00","2005-01-04T00:00:00","2005-01-05T00:00:00","2005-01-06T00:00:00","2005-01-07T00:00:00","2005-01-10T00:00:00","2005-01-11T00:00:00","2005-01-12T00:00:00","2005-01-13T00:00:00","2005-01-14T00:00:00","2005-01-18T00:00:00","2005-01-19T00:00:00","2005-01-20T00:00:00","2005-01-21T00:00:00","2005-01-24T00:00:00","2005-01-25T00:00:00","2005-01-26T00:00:00","2005-01-27T00:00:00","2005-01-28T00:00:00","2005-01-31T00:00:00","2005-02-01T00:00:00","2005-02-02T00:00:00","2005-02-03T00:00:00","2005-02-04T00:00:00","2005-02-07T00:00:00","2005-02-08T00:00:00","2005-02-09T00:00:00","2005-02-10T00:00:00","2005-02-11T00:00:00","2005-02-14T00:00:00","2005-02-15T00:00:00","2005-02-16T00:00:00","2005-02-17T00:00:00","2005-02-18T00:00:00","2005-02-22T00:00:00","2005-02-23T00:00:00","2005-02-24T00:00:00","2005-02-25T00:00:00","2005-02-28T00:00:00","2005-03-01T00:00:00","2005-03-02T00:00:00","2005-03-03T00:00:00","2005-03-04T00:00:00","2005-03-07T00:00:00","2005-03-08T00:00:00","2005-03-09T00:00:00","2005-03-10T00:00:00","2005-03-11T00:00:00","2005-03-14T00:00:00","2005-03-15T00:00:00","2005-03-16T00:00:00","2005-03-17T00:00:00","2005-03-18T00:00:00","2005-03-21T00:00:00","2005-03-22T00:00:00","2005-03-23T00:00:00","2005-03-24T00:00:00","2005-03-28T00:00:00","2005-03-29T00:00:00","2005-03-30T00:00:00","2005-03-31T00:00:00","2005-04-01T00:00:00","2005-04-04T00:00:00","2005-04-05T00:00:00","2005-04-06T00:00:00","2005-04-07T00:00:00","2005-04-08T00:00:00","2005-04-11T00:00:00","2005-04-12T00:00:00","2005-04-13T00:00:00","2005-04-14T00:00:00","2005-04-15T00:00:00","2005-04-18T00:00:00","2005-04-19T00:00:00","2005-04-20T00:00:00","2005-04-21T00:00:00","2005-04-22T00:00:00","2005-04-25T00:00:00","2005-04-26T00:00:00","2005-04-27T00:00:00","2005-04-28T00:00:00","2005-04-29T00:00:00","2005-05-02T00:00:00","2005-05-03T00:00:00","2005-05-04T00:00:00","2005-05-05T00:00:00","2005-05-06T00:00:00","2005-05-09T00:00:00","2005-05-10T00:00:00","2005-05-11T00:00:00","2005-05-12T00:00:00","2005-05-13T00:00:00","2005-05-16T00:00:00","2005-05-17T00:00:00","2005-05-18T00:00:00","2005-05-19T00:00:00","2005-05-20T00:00:00","2005-05-23T00:00:00","2005-05-24T00:00:00","2005-05-25T00:00:00","2005-05-26T00:00:00","2005-05-27T00:00:00","2005-05-31T00:00:00","2005-06-01T00:00:00","2005-06-02T00:00:00","2005-06-03T00:00:00","2005-06-06T00:00:00","2005-06-07T00:00:00","2005-06-08T00:00:00","2005-06-09T00:00:00","2005-06-10T00:00:00","2005-06-13T00:00:00","2005-06-14T00:00:00","2005-06-15T00:00:00","2005-06-16T00:00:00","2005-06-17T00:00:00","2005-06-20T00:00:00","2005-06-21T00:00:00","2005-06-22T00:00:00","2005-06-23T00:00:00","2005-06-24T00:00:00","2005-06-27T00:00:00","2005-06-28T00:00:00","2005-06-29T00:00:00","2005-06-30T00:00:00","2005-07-01T00:00:00","2005-07-05T00:00:00","2005-07-06T00:00:00","2005-07-07T00:00:00","2005-07-08T00:00:00","2005-07-11T00:00:00","2005-07-12T00:00:00","2005-07-13T00:00:00","2005-07-14T00:00:00","2005-07-15T00:00:00","2005-07-18T00:00:00","2005-07-19T00:00:00","2005-07-20T00:00:00","2005-07-21T00:00:00","2005-07-22T00:00:00","2005-07-25T00:00:00","2005-07-26T00:00:00","2005-07-27T00:00:00","2005-07-28T00:00:00","2005-07-29T00:00:00","2005-08-01T00:00:00","2005-08-02T00:00:00","2005-08-03T00:00:00","2005-08-04T00:00:00","2005-08-05T00:00:00","2005-08-08T00:00:00","2005-08-09T00:00:00","2005-08-10T00:00:00","2005-08-11T00:00:00","2005-08-12T00:00:00","2005-08-15T00:00:00","2005-08-16T00:00:00","2005-08-17T00:00:00","2005-08-18T00:00:00","2005-08-19T00:00:00","2005-08-22T00:00:00","2005-08-23T00:00:00","2005-08-24T00:00:00","2005-08-25T00:00:00","2005-08-26T00:00:00","2005-08-29T00:00:00","2005-08-30T00:00:00","2005-08-31T00:00:00","2005-09-01T00:00:00","2005-09-02T00:00:00","2005-09-06T00:00:00","2005-09-07T00:00:00","2005-09-08T00:00:00","2005-09-09T00:00:00","2005-09-12T00:00:00","2005-09-13T00:00:00","2005-09-14T00:00:00","2005-09-15T00:00:00","2005-09-16T00:00:00","2005-09-19T00:00:00","2005-09-20T00:00:00","2005-09-21T00:00:00","2005-09-22T00:00:00","2005-09-23T00:00:00","2005-09-26T00:00:00","2005-09-27T00:00:00","2005-09-28T00:00:00","2005-09-29T00:00:00","2005-09-30T00:00:00","2005-10-03T00:00:00","2005-10-04T00:00:00","2005-10-05T00:00:00","2005-10-06T00:00:00","2005-10-07T00:00:00","2005-10-10T00:00:00","2005-10-11T00:00:00","2005-10-12T00:00:00","2005-10-13T00:00:00","2005-10-14T00:00:00","2005-10-17T00:00:00","2005-10-18T00:00:00","2005-10-19T00:00:00","2005-10-20T00:00:00","2005-10-21T00:00:00","2005-10-24T00:00:00","2005-10-25T00:00:00","2005-10-26T00:00:00","2005-10-27T00:00:00","2005-10-28T00:00:00","2005-10-31T00:00:00","2005-11-01T00:00:00","2005-11-02T00:00:00","2005-11-03T00:00:00","2005-11-04T00:00:00","2005-11-07T00:00:00","2005-11-08T00:00:00","2005-11-09T00:00:00","2005-11-10T00:00:00","2005-11-11T00:00:00","2005-11-14T00:00:00","2005-11-15T00:00:00","2005-11-16T00:00:00","2005-11-17T00:00:00","2005-11-18T00:00:00","2005-11-21T00:00:00","2005-11-22T00:00:00","2005-11-23T00:00:00","2005-11-25T00:00:00","2005-11-28T00:00:00","2005-11-29T00:00:00","2005-11-30T00:00:00","2005-12-01T00:00:00","2005-12-02T00:00:00","2005-12-05T00:00:00","2005-12-06T00:00:00","2005-12-07T00:00:00","2005-12-08T00:00:00","2005-12-09T00:00:00","2005-12-12T00:00:00","2005-12-13T00:00:00","2005-12-14T00:00:00","2005-12-15T00:00:00","2005-12-16T00:00:00","2005-12-19T00:00:00","2005-12-20T00:00:00","2005-12-21T00:00:00","2005-12-22T00:00:00","2005-12-23T00:00:00","2005-12-27T00:00:00","2005-12-28T00:00:00","2005-12-29T00:00:00","2005-12-30T00:00:00","2006-01-03T00:00:00","2006-01-04T00:00:00","2006-01-05T00:00:00","2006-01-06T00:00:00","2006-01-09T00:00:00","2006-01-10T00:00:00","2006-01-11T00:00:00","2006-01-12T00:00:00","2006-01-13T00:00:00","2006-01-17T00:00:00","2006-01-18T00:00:00","2006-01-19T00:00:00","2006-01-20T00:00:00","2006-01-23T00:00:00","2006-01-24T00:00:00","2006-01-25T00:00:00","2006-01-26T00:00:00","2006-01-27T00:00:00","2006-01-30T00:00:00","2006-01-31T00:00:00","2006-02-01T00:00:00","2006-02-02T00:00:00","2006-02-03T00:00:00","2006-02-06T00:00:00","2006-02-07T00:00:00","2006-02-08T00:00:00","2006-02-09T00:00:00","2006-02-10T00:00:00","2006-02-13T00:00:00","2006-02-14T00:00:00","2006-02-15T00:00:00","2006-02-16T00:00:00","2006-02-17T00:00:00","2006-02-21T00:00:00","2006-02-22T00:00:00","2006-02-23T00:00:00","2006-02-24T00:00:00","2006-02-27T00:00:00","2006-02-28T00:00:00","2006-03-01T00:00:00","2006-03-02T00:00:00","2006-03-03T00:00:00","2006-03-06T00:00:00","2006-03-07T00:00:00","2006-03-08T00:00:00","2006-03-09T00:00:00","2006-03-10T00:00:00","2006-03-13T00:00:00","2006-03-14T00:00:00","2006-03-15T00:00:00","2006-03-16T00:00:00","2006-03-17T00:00:00","2006-03-20T00:00:00","2006-03-21T00:00:00","2006-03-22T00:00:00","2006-03-23T00:00:00","2006-03-24T00:00:00","2006-03-27T00:00:00","2006-03-28T00:00:00","2006-03-29T00:00:00","2006-03-30T00:00:00","2006-03-31T00:00:00","2006-04-03T00:00:00","2006-04-04T00:00:00","2006-04-05T00:00:00","2006-04-06T00:00:00","2006-04-07T00:00:00","2006-04-10T00:00:00","2006-04-11T00:00:00","2006-04-12T00:00:00","2006-04-13T00:00:00","2006-04-17T00:00:00","2006-04-18T00:00:00","2006-04-19T00:00:00","2006-04-20T00:00:00","2006-04-21T00:00:00","2006-04-24T00:00:00","2006-04-25T00:00:00","2006-04-26T00:00:00","2006-04-27T00:00:00","2006-04-28T00:00:00","2006-05-01T00:00:00","2006-05-02T00:00:00","2006-05-03T00:00:00","2006-05-04T00:00:00","2006-05-05T00:00:00","2006-05-08T00:00:00","2006-05-09T00:00:00","2006-05-10T00:00:00","2006-05-11T00:00:00","2006-05-12T00:00:00","2006-05-15T00:00:00","2006-05-16T00:00:00","2006-05-17T00:00:00","2006-05-18T00:00:00","2006-05-19T00:00:00","2006-05-22T00:00:00","2006-05-23T00:00:00","2006-05-24T00:00:00","2006-05-25T00:00:00","2006-05-26T00:00:00","2006-05-30T00:00:00","2006-05-31T00:00:00","2006-06-01T00:00:00","2006-06-02T00:00:00","2006-06-05T00:00:00","2006-06-06T00:00:00","2006-06-07T00:00:00","2006-06-08T00:00:00","2006-06-09T00:00:00","2006-06-12T00:00:00","2006-06-13T00:00:00","2006-06-14T00:00:00","2006-06-15T00:00:00","2006-06-16T00:00:00","2006-06-19T00:00:00","2006-06-20T00:00:00","2006-06-21T00:00:00","2006-06-22T00:00:00","2006-06-23T00:00:00","2006-06-26T00:00:00","2006-06-27T00:00:00","2006-06-28T00:00:00","2006-06-29T00:00:00","2006-06-30T00:00:00","2006-07-03T00:00:00","2006-07-05T00:00:00","2006-07-06T00:00:00","2006-07-07T00:00:00","2006-07-10T00:00:00","2006-07-11T00:00:00","2006-07-12T00:00:00","2006-07-13T00:00:00","2006-07-14T00:00:00","2006-07-17T00:00:00","2006-07-18T00:00:00","2006-07-19T00:00:00","2006-07-20T00:00:00","2006-07-21T00:00:00","2006-07-24T00:00:00","2006-07-25T00:00:00","2006-07-26T00:00:00","2006-07-27T00:00:00","2006-07-28T00:00:00","2006-07-31T00:00:00","2006-08-01T00:00:00","2006-08-02T00:00:00","2006-08-03T00:00:00","2006-08-04T00:00:00","2006-08-07T00:00:00","2006-08-08T00:00:00","2006-08-09T00:00:00","2006-08-10T00:00:00","2006-08-11T00:00:00","2006-08-14T00:00:00","2006-08-15T00:00:00","2006-08-16T00:00:00","2006-08-17T00:00:00","2006-08-18T00:00:00","2006-08-21T00:00:00","2006-08-22T00:00:00","2006-08-23T00:00:00","2006-08-24T00:00:00","2006-08-25T00:00:00","2006-08-28T00:00:00","2006-08-29T00:00:00","2006-08-30T00:00:00","2006-08-31T00:00:00","2006-09-01T00:00:00","2006-09-05T00:00:00","2006-09-06T00:00:00","2006-09-07T00:00:00","2006-09-08T00:00:00","2006-09-11T00:00:00","2006-09-12T00:00:00","2006-09-13T00:00:00","2006-09-14T00:00:00","2006-09-15T00:00:00","2006-09-18T00:00:00","2006-09-19T00:00:00","2006-09-20T00:00:00","2006-09-21T00:00:00","2006-09-22T00:00:00","2006-09-25T00:00:00","2006-09-26T00:00:00","2006-09-27T00:00:00","2006-09-28T00:00:00","2006-09-29T00:00:00","2006-10-02T00:00:00","2006-10-03T00:00:00","2006-10-04T00:00:00","2006-10-05T00:00:00","2006-10-06T00:00:00","2006-10-09T00:00:00","2006-10-10T00:00:00","2006-10-11T00:00:00","2006-10-12T00:00:00","2006-10-13T00:00:00","2006-10-16T00:00:00","2006-10-17T00:00:00","2006-10-18T00:00:00","2006-10-19T00:00:00","2006-10-20T00:00:00","2006-10-23T00:00:00","2006-10-24T00:00:00","2006-10-25T00:00:00","2006-10-26T00:00:00","2006-10-27T00:00:00","2006-10-30T00:00:00","2006-10-31T00:00:00","2006-11-01T00:00:00","2006-11-02T00:00:00","2006-11-03T00:00:00","2006-11-06T00:00:00","2006-11-07T00:00:00","2006-11-08T00:00:00","2006-11-09T00:00:00","2006-11-10T00:00:00","2006-11-13T00:00:00","2006-11-14T00:00:00","2006-11-15T00:00:00","2006-11-16T00:00:00","2006-11-17T00:00:00","2006-11-20T00:00:00","2006-11-21T00:00:00","2006-11-22T00:00:00","2006-11-24T00:00:00","2006-11-27T00:00:00","2006-11-28T00:00:00","2006-11-29T00:00:00","2006-11-30T00:00:00","2006-12-01T00:00:00","2006-12-04T00:00:00","2006-12-05T00:00:00","2006-12-06T00:00:00","2006-12-07T00:00:00","2006-12-08T00:00:00","2006-12-11T00:00:00","2006-12-12T00:00:00","2006-12-13T00:00:00","2006-12-14T00:00:00","2006-12-15T00:00:00","2006-12-18T00:00:00","2006-12-19T00:00:00","2006-12-20T00:00:00","2006-12-21T00:00:00","2006-12-22T00:00:00","2006-12-26T00:00:00","2006-12-27T00:00:00","2006-12-28T00:00:00","2006-12-29T00:00:00","2007-01-03T00:00:00","2007-01-04T00:00:00","2007-01-05T00:00:00","2007-01-08T00:00:00","2007-01-09T00:00:00","2007-01-10T00:00:00","2007-01-11T00:00:00","2007-01-12T00:00:00","2007-01-16T00:00:00","2007-01-17T00:00:00","2007-01-18T00:00:00","2007-01-19T00:00:00","2007-01-22T00:00:00","2007-01-23T00:00:00","2007-01-24T00:00:00","2007-01-25T00:00:00","2007-01-26T00:00:00","2007-01-29T00:00:00","2007-01-30T00:00:00","2007-01-31T00:00:00","2007-02-01T00:00:00","2007-02-02T00:00:00","2007-02-05T00:00:00","2007-02-06T00:00:00","2007-02-07T00:00:00","2007-02-08T00:00:00","2007-02-09T00:00:00","2007-02-12T00:00:00","2007-02-13T00:00:00","2007-02-14T00:00:00","2007-02-15T00:00:00","2007-02-16T00:00:00","2007-02-20T00:00:00","2007-02-21T00:00:00","2007-02-22T00:00:00","2007-02-23T00:00:00","2007-02-26T00:00:00","2007-02-27T00:00:00","2007-02-28T00:00:00","2007-03-01T00:00:00","2007-03-02T00:00:00","2007-03-05T00:00:00","2007-03-06T00:00:00","2007-03-07T00:00:00","2007-03-08T00:00:00","2007-03-09T00:00:00","2007-03-12T00:00:00","2007-03-13T00:00:00","2007-03-14T00:00:00","2007-03-15T00:00:00","2007-03-16T00:00:00","2007-03-19T00:00:00","2007-03-20T00:00:00","2007-03-21T00:00:00","2007-03-22T00:00:00","2007-03-23T00:00:00","2007-03-26T00:00:00","2007-03-27T00:00:00","2007-03-28T00:00:00","2007-03-29T00:00:00","2007-03-30T00:00:00","2007-04-02T00:00:00","2007-04-03T00:00:00","2007-04-04T00:00:00","2007-04-05T00:00:00","2007-04-09T00:00:00","2007-04-10T00:00:00","2007-04-11T00:00:00","2007-04-12T00:00:00","2007-04-13T00:00:00","2007-04-16T00:00:00","2007-04-17T00:00:00","2007-04-18T00:00:00","2007-04-19T00:00:00","2007-04-20T00:00:00","2007-04-23T00:00:00","2007-04-24T00:00:00","2007-04-25T00:00:00","2007-04-26T00:00:00","2007-04-27T00:00:00","2007-04-30T00:00:00","2007-05-01T00:00:00","2007-05-02T00:00:00","2007-05-03T00:00:00","2007-05-04T00:00:00","2007-05-07T00:00:00","2007-05-08T00:00:00","2007-05-09T00:00:00","2007-05-10T00:00:00","2007-05-11T00:00:00","2007-05-14T00:00:00","2007-05-15T00:00:00","2007-05-16T00:00:00","2007-05-17T00:00:00","2007-05-18T00:00:00","2007-05-21T00:00:00","2007-05-22T00:00:00","2007-05-23T00:00:00","2007-05-24T00:00:00","2007-05-25T00:00:00","2007-05-29T00:00:00","2007-05-30T00:00:00","2007-05-31T00:00:00","2007-06-01T00:00:00","2007-06-04T00:00:00","2007-06-05T00:00:00","2007-06-06T00:00:00","2007-06-07T00:00:00","2007-06-08T00:00:00","2007-06-11T00:00:00","2007-06-12T00:00:00","2007-06-13T00:00:00","2007-06-14T00:00:00","2007-06-15T00:00:00","2007-06-18T00:00:00","2007-06-19T00:00:00","2007-06-20T00:00:00","2007-06-21T00:00:00","2007-06-22T00:00:00","2007-06-25T00:00:00","2007-06-26T00:00:00","2007-06-27T00:00:00","2007-06-28T00:00:00","2007-06-29T00:00:00","2007-07-02T00:00:00","2007-07-03T00:00:00","2007-07-05T00:00:00","2007-07-06T00:00:00","2007-07-09T00:00:00","2007-07-10T00:00:00","2007-07-11T00:00:00","2007-07-12T00:00:00","2007-07-13T00:00:00","2007-07-16T00:00:00","2007-07-17T00:00:00","2007-07-18T00:00:00","2007-07-19T00:00:00","2007-07-20T00:00:00","2007-07-23T00:00:00","2007-07-24T00:00:00","2007-07-25T00:00:00","2007-07-26T00:00:00","2007-07-27T00:00:00","2007-07-30T00:00:00","2007-07-31T00:00:00","2007-08-01T00:00:00","2007-08-02T00:00:00","2007-08-03T00:00:00","2007-08-06T00:00:00","2007-08-07T00:00:00","2007-08-08T00:00:00","2007-08-09T00:00:00","2007-08-10T00:00:00","2007-08-13T00:00:00","2007-08-14T00:00:00","2007-08-15T00:00:00","2007-08-16T00:00:00","2007-08-17T00:00:00","2007-08-20T00:00:00","2007-08-21T00:00:00","2007-08-22T00:00:00","2007-08-23T00:00:00","2007-08-24T00:00:00","2007-08-27T00:00:00","2007-08-28T00:00:00","2007-08-29T00:00:00","2007-08-30T00:00:00","2007-08-31T00:00:00","2007-09-04T00:00:00","2007-09-05T00:00:00","2007-09-06T00:00:00","2007-09-07T00:00:00","2007-09-10T00:00:00","2007-09-11T00:00:00","2007-09-12T00:00:00","2007-09-13T00:00:00","2007-09-14T00:00:00","2007-09-17T00:00:00","2007-09-18T00:00:00","2007-09-19T00:00:00","2007-09-20T00:00:00","2007-09-21T00:00:00","2007-09-24T00:00:00","2007-09-25T00:00:00","2007-09-26T00:00:00","2007-09-27T00:00:00","2007-09-28T00:00:00","2007-10-01T00:00:00","2007-10-02T00:00:00","2007-10-03T00:00:00","2007-10-04T00:00:00","2007-10-05T00:00:00","2007-10-08T00:00:00","2007-10-09T00:00:00","2007-10-10T00:00:00","2007-10-11T00:00:00","2007-10-12T00:00:00","2007-10-15T00:00:00","2007-10-16T00:00:00","2007-10-17T00:00:00","2007-10-18T00:00:00","2007-10-19T00:00:00","2007-10-22T00:00:00","2007-10-23T00:00:00","2007-10-24T00:00:00","2007-10-25T00:00:00","2007-10-26T00:00:00","2007-10-29T00:00:00","2007-10-30T00:00:00","2007-10-31T00:00:00","2007-11-01T00:00:00","2007-11-02T00:00:00","2007-11-05T00:00:00","2007-11-06T00:00:00","2007-11-07T00:00:00","2007-11-08T00:00:00","2007-11-09T00:00:00","2007-11-12T00:00:00","2007-11-13T00:00:00","2007-11-14T00:00:00","2007-11-15T00:00:00","2007-11-16T00:00:00","2007-11-19T00:00:00","2007-11-20T00:00:00","2007-11-21T00:00:00","2007-11-23T00:00:00","2007-11-26T00:00:00","2007-11-27T00:00:00","2007-11-28T00:00:00","2007-11-29T00:00:00","2007-11-30T00:00:00","2007-12-03T00:00:00","2007-12-04T00:00:00","2007-12-05T00:00:00","2007-12-06T00:00:00","2007-12-07T00:00:00","2007-12-10T00:00:00","2007-12-11T00:00:00","2007-12-12T00:00:00","2007-12-13T00:00:00","2007-12-14T00:00:00","2007-12-17T00:00:00","2007-12-18T00:00:00","2007-12-19T00:00:00","2007-12-20T00:00:00","2007-12-21T00:00:00","2007-12-24T00:00:00","2007-12-26T00:00:00","2007-12-27T00:00:00","2007-12-28T00:00:00","2007-12-31T00:00:00","2008-01-02T00:00:00","2008-01-03T00:00:00","2008-01-04T00:00:00","2008-01-07T00:00:00","2008-01-08T00:00:00","2008-01-09T00:00:00","2008-01-10T00:00:00","2008-01-11T00:00:00","2008-01-14T00:00:00","2008-01-15T00:00:00","2008-01-16T00:00:00","2008-01-17T00:00:00","2008-01-18T00:00:00","2008-01-22T00:00:00","2008-01-23T00:00:00","2008-01-24T00:00:00","2008-01-25T00:00:00","2008-01-28T00:00:00","2008-01-29T00:00:00","2008-01-30T00:00:00","2008-01-31T00:00:00","2008-02-01T00:00:00","2008-02-04T00:00:00","2008-02-05T00:00:00","2008-02-06T00:00:00","2008-02-07T00:00:00","2008-02-08T00:00:00","2008-02-11T00:00:00","2008-02-12T00:00:00","2008-02-13T00:00:00","2008-02-14T00:00:00","2008-02-15T00:00:00","2008-02-19T00:00:00","2008-02-20T00:00:00","2008-02-21T00:00:00","2008-02-22T00:00:00","2008-02-25T00:00:00","2008-02-26T00:00:00","2008-02-27T00:00:00","2008-02-28T00:00:00","2008-02-29T00:00:00","2008-03-03T00:00:00","2008-03-04T00:00:00","2008-03-05T00:00:00","2008-03-06T00:00:00","2008-03-07T00:00:00","2008-03-10T00:00:00","2008-03-11T00:00:00","2008-03-12T00:00:00","2008-03-13T00:00:00","2008-03-14T00:00:00","2008-03-17T00:00:00","2008-03-18T00:00:00","2008-03-19T00:00:00","2008-03-20T00:00:00","2008-03-24T00:00:00","2008-03-25T00:00:00","2008-03-26T00:00:00","2008-03-27T00:00:00","2008-03-28T00:00:00","2008-03-31T00:00:00","2008-04-01T00:00:00","2008-04-02T00:00:00","2008-04-03T00:00:00","2008-04-04T00:00:00","2008-04-07T00:00:00","2008-04-08T00:00:00","2008-04-09T00:00:00","2008-04-10T00:00:00","2008-04-11T00:00:00","2008-04-14T00:00:00","2008-04-15T00:00:00","2008-04-16T00:00:00","2008-04-17T00:00:00","2008-04-18T00:00:00","2008-04-21T00:00:00","2008-04-22T00:00:00","2008-04-23T00:00:00","2008-04-24T00:00:00","2008-04-25T00:00:00","2008-04-28T00:00:00","2008-04-29T00:00:00","2008-04-30T00:00:00","2008-05-01T00:00:00","2008-05-02T00:00:00","2008-05-05T00:00:00","2008-05-06T00:00:00","2008-05-07T00:00:00","2008-05-08T00:00:00","2008-05-09T00:00:00","2008-05-12T00:00:00","2008-05-13T00:00:00","2008-05-14T00:00:00","2008-05-15T00:00:00","2008-05-16T00:00:00","2008-05-19T00:00:00","2008-05-20T00:00:00","2008-05-21T00:00:00","2008-05-22T00:00:00","2008-05-23T00:00:00","2008-05-27T00:00:00","2008-05-28T00:00:00","2008-05-29T00:00:00","2008-05-30T00:00:00","2008-06-02T00:00:00","2008-06-03T00:00:00","2008-06-04T00:00:00","2008-06-05T00:00:00","2008-06-06T00:00:00","2008-06-09T00:00:00","2008-06-10T00:00:00","2008-06-11T00:00:00","2008-06-12T00:00:00","2008-06-13T00:00:00","2008-06-16T00:00:00","2008-06-17T00:00:00","2008-06-18T00:00:00","2008-06-19T00:00:00","2008-06-20T00:00:00","2008-06-23T00:00:00","2008-06-24T00:00:00","2008-06-25T00:00:00","2008-06-26T00:00:00","2008-06-27T00:00:00","2008-06-30T00:00:00","2008-07-01T00:00:00","2008-07-02T00:00:00","2008-07-03T00:00:00","2008-07-07T00:00:00","2008-07-08T00:00:00","2008-07-09T00:00:00","2008-07-10T00:00:00","2008-07-11T00:00:00","2008-07-14T00:00:00","2008-07-15T00:00:00","2008-07-16T00:00:00","2008-07-17T00:00:00","2008-07-18T00:00:00","2008-07-21T00:00:00","2008-07-22T00:00:00","2008-07-23T00:00:00","2008-07-24T00:00:00","2008-07-25T00:00:00","2008-07-28T00:00:00","2008-07-29T00:00:00","2008-07-30T00:00:00","2008-07-31T00:00:00","2008-08-01T00:00:00","2008-08-04T00:00:00","2008-08-05T00:00:00","2008-08-06T00:00:00","2008-08-07T00:00:00","2008-08-08T00:00:00","2008-08-11T00:00:00","2008-08-12T00:00:00","2008-08-13T00:00:00","2008-08-14T00:00:00","2008-08-15T00:00:00","2008-08-18T00:00:00","2008-08-19T00:00:00","2008-08-20T00:00:00","2008-08-21T00:00:00","2008-08-22T00:00:00","2008-08-25T00:00:00","2008-08-26T00:00:00","2008-08-27T00:00:00","2008-08-28T00:00:00","2008-08-29T00:00:00","2008-09-02T00:00:00","2008-09-03T00:00:00","2008-09-04T00:00:00","2008-09-05T00:00:00","2008-09-08T00:00:00","2008-09-09T00:00:00","2008-09-10T00:00:00","2008-09-11T00:00:00","2008-09-12T00:00:00","2008-09-15T00:00:00","2008-09-16T00:00:00","2008-09-17T00:00:00","2008-09-18T00:00:00","2008-09-19T00:00:00","2008-09-22T00:00:00","2008-09-23T00:00:00","2008-09-24T00:00:00","2008-09-25T00:00:00","2008-09-26T00:00:00","2008-09-29T00:00:00","2008-09-30T00:00:00","2008-10-01T00:00:00","2008-10-02T00:00:00","2008-10-03T00:00:00","2008-10-06T00:00:00","2008-10-07T00:00:00","2008-10-08T00:00:00","2008-10-09T00:00:00","2008-10-10T00:00:00","2008-10-13T00:00:00","2008-10-14T00:00:00","2008-10-15T00:00:00","2008-10-16T00:00:00","2008-10-17T00:00:00","2008-10-20T00:00:00","2008-10-21T00:00:00","2008-10-22T00:00:00","2008-10-23T00:00:00","2008-10-24T00:00:00","2008-10-27T00:00:00","2008-10-28T00:00:00","2008-10-29T00:00:00","2008-10-30T00:00:00","2008-10-31T00:00:00","2008-11-03T00:00:00","2008-11-04T00:00:00","2008-11-05T00:00:00","2008-11-06T00:00:00","2008-11-07T00:00:00","2008-11-10T00:00:00","2008-11-11T00:00:00","2008-11-12T00:00:00","2008-11-13T00:00:00","2008-11-14T00:00:00","2008-11-17T00:00:00","2008-11-18T00:00:00","2008-11-19T00:00:00","2008-11-20T00:00:00","2008-11-21T00:00:00","2008-11-24T00:00:00","2008-11-25T00:00:00","2008-11-26T00:00:00","2008-11-28T00:00:00","2008-12-01T00:00:00","2008-12-02T00:00:00","2008-12-03T00:00:00","2008-12-04T00:00:00","2008-12-05T00:00:00","2008-12-08T00:00:00","2008-12-09T00:00:00","2008-12-10T00:00:00","2008-12-11T00:00:00","2008-12-12T00:00:00","2008-12-15T00:00:00","2008-12-16T00:00:00","2008-12-17T00:00:00","2008-12-18T00:00:00","2008-12-19T00:00:00","2008-12-22T00:00:00","2008-12-23T00:00:00","2008-12-24T00:00:00","2008-12-26T00:00:00","2008-12-29T00:00:00","2008-12-30T00:00:00","2008-12-31T00:00:00","2009-01-02T00:00:00","2009-01-05T00:00:00","2009-01-06T00:00:00","2009-01-07T00:00:00","2009-01-08T00:00:00","2009-01-09T00:00:00","2009-01-12T00:00:00","2009-01-13T00:00:00","2009-01-14T00:00:00","2009-01-15T00:00:00","2009-01-16T00:00:00","2009-01-20T00:00:00","2009-01-21T00:00:00","2009-01-22T00:00:00","2009-01-23T00:00:00","2009-01-26T00:00:00","2009-01-27T00:00:00","2009-01-28T00:00:00","2009-01-29T00:00:00","2009-01-30T00:00:00","2009-02-02T00:00:00","2009-02-03T00:00:00","2009-02-04T00:00:00","2009-02-05T00:00:00","2009-02-06T00:00:00","2009-02-09T00:00:00","2009-02-10T00:00:00","2009-02-11T00:00:00","2009-02-12T00:00:00","2009-02-13T00:00:00","2009-02-17T00:00:00","2009-02-18T00:00:00","2009-02-19T00:00:00","2009-02-20T00:00:00","2009-02-23T00:00:00","2009-02-24T00:00:00","2009-02-25T00:00:00","2009-02-26T00:00:00","2009-02-27T00:00:00","2009-03-02T00:00:00","2009-03-03T00:00:00","2009-03-04T00:00:00","2009-03-05T00:00:00","2009-03-06T00:00:00","2009-03-09T00:00:00","2009-03-10T00:00:00","2009-03-11T00:00:00","2009-03-12T00:00:00","2009-03-13T00:00:00","2009-03-16T00:00:00","2009-03-17T00:00:00","2009-03-18T00:00:00","2009-03-19T00:00:00","2009-03-20T00:00:00","2009-03-23T00:00:00","2009-03-24T00:00:00","2009-03-25T00:00:00","2009-03-26T00:00:00","2009-03-27T00:00:00","2009-03-30T00:00:00","2009-03-31T00:00:00","2009-04-01T00:00:00","2009-04-02T00:00:00","2009-04-03T00:00:00","2009-04-06T00:00:00","2009-04-07T00:00:00","2009-04-08T00:00:00","2009-04-09T00:00:00","2009-04-13T00:00:00","2009-04-14T00:00:00","2009-04-15T00:00:00","2009-04-16T00:00:00","2009-04-17T00:00:00","2009-04-20T00:00:00","2009-04-21T00:00:00","2009-04-22T00:00:00","2009-04-23T00:00:00","2009-04-24T00:00:00","2009-04-27T00:00:00","2009-04-28T00:00:00","2009-04-29T00:00:00","2009-04-30T00:00:00","2009-05-01T00:00:00","2009-05-04T00:00:00","2009-05-05T00:00:00","2009-05-06T00:00:00","2009-05-07T00:00:00","2009-05-08T00:00:00","2009-05-11T00:00:00","2009-05-12T00:00:00","2009-05-13T00:00:00","2009-05-14T00:00:00","2009-05-15T00:00:00","2009-05-18T00:00:00","2009-05-19T00:00:00","2009-05-20T00:00:00","2009-05-21T00:00:00","2009-05-22T00:00:00","2009-05-26T00:00:00","2009-05-27T00:00:00","2009-05-28T00:00:00","2009-05-29T00:00:00","2009-06-01T00:00:00","2009-06-02T00:00:00","2009-06-03T00:00:00","2009-06-04T00:00:00","2009-06-05T00:00:00","2009-06-08T00:00:00","2009-06-09T00:00:00","2009-06-10T00:00:00","2009-06-11T00:00:00","2009-06-12T00:00:00","2009-06-15T00:00:00","2009-06-16T00:00:00","2009-06-17T00:00:00","2009-06-18T00:00:00","2009-06-19T00:00:00","2009-06-22T00:00:00","2009-06-23T00:00:00","2009-06-24T00:00:00","2009-06-25T00:00:00","2009-06-26T00:00:00","2009-06-29T00:00:00","2009-06-30T00:00:00","2009-07-01T00:00:00","2009-07-02T00:00:00","2009-07-06T00:00:00","2009-07-07T00:00:00","2009-07-08T00:00:00","2009-07-09T00:00:00","2009-07-10T00:00:00","2009-07-13T00:00:00","2009-07-14T00:00:00","2009-07-15T00:00:00","2009-07-16T00:00:00","2009-07-17T00:00:00","2009-07-20T00:00:00","2009-07-21T00:00:00","2009-07-22T00:00:00","2009-07-23T00:00:00","2009-07-24T00:00:00","2009-07-27T00:00:00","2009-07-28T00:00:00","2009-07-29T00:00:00","2009-07-30T00:00:00","2009-07-31T00:00:00","2009-08-03T00:00:00","2009-08-04T00:00:00","2009-08-05T00:00:00","2009-08-06T00:00:00","2009-08-07T00:00:00","2009-08-10T00:00:00","2009-08-11T00:00:00","2009-08-12T00:00:00","2009-08-13T00:00:00","2009-08-14T00:00:00","2009-08-17T00:00:00","2009-08-18T00:00:00","2009-08-19T00:00:00","2009-08-20T00:00:00","2009-08-21T00:00:00","2009-08-24T00:00:00","2009-08-25T00:00:00","2009-08-26T00:00:00","2009-08-27T00:00:00","2009-08-28T00:00:00","2009-08-31T00:00:00","2009-09-01T00:00:00","2009-09-02T00:00:00","2009-09-03T00:00:00","2009-09-04T00:00:00","2009-09-08T00:00:00","2009-09-09T00:00:00","2009-09-10T00:00:00","2009-09-11T00:00:00","2009-09-14T00:00:00","2009-09-15T00:00:00","2009-09-16T00:00:00","2009-09-17T00:00:00","2009-09-18T00:00:00","2009-09-21T00:00:00","2009-09-22T00:00:00","2009-09-23T00:00:00","2009-09-24T00:00:00","2009-09-25T00:00:00","2009-09-28T00:00:00","2009-09-29T00:00:00","2009-09-30T00:00:00","2009-10-01T00:00:00","2009-10-02T00:00:00","2009-10-05T00:00:00","2009-10-06T00:00:00","2009-10-07T00:00:00","2009-10-08T00:00:00","2009-10-09T00:00:00","2009-10-12T00:00:00","2009-10-13T00:00:00","2009-10-14T00:00:00","2009-10-15T00:00:00","2009-10-16T00:00:00","2009-10-19T00:00:00","2009-10-20T00:00:00","2009-10-21T00:00:00","2009-10-22T00:00:00","2009-10-23T00:00:00","2009-10-26T00:00:00","2009-10-27T00:00:00","2009-10-28T00:00:00","2009-10-29T00:00:00","2009-10-30T00:00:00","2009-11-02T00:00:00","2009-11-03T00:00:00","2009-11-04T00:00:00","2009-11-05T00:00:00","2009-11-06T00:00:00","2009-11-09T00:00:00","2009-11-10T00:00:00","2009-11-11T00:00:00","2009-11-12T00:00:00","2009-11-13T00:00:00","2009-11-16T00:00:00","2009-11-17T00:00:00","2009-11-18T00:00:00","2009-11-19T00:00:00","2009-11-20T00:00:00","2009-11-23T00:00:00","2009-11-24T00:00:00","2009-11-25T00:00:00","2009-11-27T00:00:00","2009-11-30T00:00:00","2009-12-01T00:00:00","2009-12-02T00:00:00","2009-12-03T00:00:00","2009-12-04T00:00:00","2009-12-07T00:00:00","2009-12-08T00:00:00","2009-12-09T00:00:00","2009-12-10T00:00:00","2009-12-11T00:00:00","2009-12-14T00:00:00","2009-12-15T00:00:00","2009-12-16T00:00:00","2009-12-17T00:00:00","2009-12-18T00:00:00","2009-12-21T00:00:00","2009-12-22T00:00:00","2009-12-23T00:00:00","2009-12-24T00:00:00","2009-12-28T00:00:00","2009-12-29T00:00:00","2009-12-30T00:00:00","2009-12-31T00:00:00","2010-01-04T00:00:00","2010-01-05T00:00:00","2010-01-06T00:00:00","2010-01-07T00:00:00","2010-01-08T00:00:00","2010-01-11T00:00:00","2010-01-12T00:00:00","2010-01-13T00:00:00","2010-01-14T00:00:00","2010-01-15T00:00:00","2010-01-19T00:00:00","2010-01-20T00:00:00","2010-01-21T00:00:00","2010-01-22T00:00:00","2010-01-25T00:00:00","2010-01-26T00:00:00","2010-01-27T00:00:00","2010-01-28T00:00:00","2010-01-29T00:00:00","2010-02-01T00:00:00","2010-02-02T00:00:00","2010-02-03T00:00:00","2010-02-04T00:00:00","2010-02-05T00:00:00","2010-02-08T00:00:00","2010-02-09T00:00:00","2010-02-10T00:00:00","2010-02-11T00:00:00","2010-02-12T00:00:00","2010-02-16T00:00:00","2010-02-17T00:00:00","2010-02-18T00:00:00","2010-02-19T00:00:00","2010-02-22T00:00:00","2010-02-23T00:00:00","2010-02-24T00:00:00","2010-02-25T00:00:00","2010-02-26T00:00:00","2010-03-01T00:00:00","2010-03-02T00:00:00","2010-03-03T00:00:00","2010-03-04T00:00:00","2010-03-05T00:00:00","2010-03-08T00:00:00","2010-03-09T00:00:00","2010-03-10T00:00:00","2010-03-11T00:00:00","2010-03-12T00:00:00","2010-03-15T00:00:00","2010-03-16T00:00:00","2010-03-17T00:00:00","2010-03-18T00:00:00","2010-03-19T00:00:00","2010-03-22T00:00:00","2010-03-23T00:00:00","2010-03-24T00:00:00","2010-03-25T00:00:00","2010-03-26T00:00:00","2010-03-29T00:00:00","2010-03-30T00:00:00","2010-03-31T00:00:00","2010-04-01T00:00:00","2010-04-05T00:00:00","2010-04-06T00:00:00","2010-04-07T00:00:00","2010-04-08T00:00:00","2010-04-09T00:00:00","2010-04-12T00:00:00","2010-04-13T00:00:00","2010-04-14T00:00:00","2010-04-15T00:00:00","2010-04-16T00:00:00","2010-04-19T00:00:00","2010-04-20T00:00:00","2010-04-21T00:00:00","2010-04-22T00:00:00","2010-04-23T00:00:00","2010-04-26T00:00:00","2010-04-27T00:00:00","2010-04-28T00:00:00","2010-04-29T00:00:00","2010-04-30T00:00:00","2010-05-03T00:00:00","2010-05-04T00:00:00","2010-05-05T00:00:00","2010-05-06T00:00:00","2010-05-07T00:00:00","2010-05-10T00:00:00","2010-05-11T00:00:00","2010-05-12T00:00:00","2010-05-13T00:00:00","2010-05-14T00:00:00","2010-05-17T00:00:00","2010-05-18T00:00:00","2010-05-19T00:00:00","2010-05-20T00:00:00","2010-05-21T00:00:00","2010-05-24T00:00:00","2010-05-25T00:00:00","2010-05-26T00:00:00","2010-05-27T00:00:00","2010-05-28T00:00:00","2010-06-01T00:00:00","2010-06-02T00:00:00","2010-06-03T00:00:00","2010-06-04T00:00:00","2010-06-07T00:00:00","2010-06-08T00:00:00","2010-06-09T00:00:00","2010-06-10T00:00:00","2010-06-11T00:00:00","2010-06-14T00:00:00","2010-06-15T00:00:00","2010-06-16T00:00:00","2010-06-17T00:00:00","2010-06-18T00:00:00","2010-06-21T00:00:00","2010-06-22T00:00:00","2010-06-23T00:00:00","2010-06-24T00:00:00","2010-06-25T00:00:00","2010-06-28T00:00:00","2010-06-29T00:00:00","2010-06-30T00:00:00","2010-07-01T00:00:00","2010-07-02T00:00:00","2010-07-06T00:00:00","2010-07-07T00:00:00","2010-07-08T00:00:00","2010-07-09T00:00:00","2010-07-12T00:00:00","2010-07-13T00:00:00","2010-07-14T00:00:00","2010-07-15T00:00:00","2010-07-16T00:00:00","2010-07-19T00:00:00","2010-07-20T00:00:00","2010-07-21T00:00:00","2010-07-22T00:00:00","2010-07-23T00:00:00","2010-07-26T00:00:00","2010-07-27T00:00:00","2010-07-28T00:00:00","2010-07-29T00:00:00","2010-07-30T00:00:00","2010-08-02T00:00:00","2010-08-03T00:00:00","2010-08-04T00:00:00","2010-08-05T00:00:00","2010-08-06T00:00:00","2010-08-09T00:00:00","2010-08-10T00:00:00","2010-08-11T00:00:00","2010-08-12T00:00:00","2010-08-13T00:00:00","2010-08-16T00:00:00","2010-08-17T00:00:00","2010-08-18T00:00:00","2010-08-19T00:00:00","2010-08-20T00:00:00","2010-08-23T00:00:00","2010-08-24T00:00:00","2010-08-25T00:00:00","2010-08-26T00:00:00","2010-08-27T00:00:00","2010-08-30T00:00:00","2010-08-31T00:00:00","2010-09-01T00:00:00","2010-09-02T00:00:00","2010-09-03T00:00:00","2010-09-07T00:00:00","2010-09-08T00:00:00","2010-09-09T00:00:00","2010-09-10T00:00:00","2010-09-13T00:00:00","2010-09-14T00:00:00","2010-09-15T00:00:00","2010-09-16T00:00:00","2010-09-17T00:00:00","2010-09-20T00:00:00","2010-09-21T00:00:00","2010-09-22T00:00:00","2010-09-23T00:00:00","2010-09-24T00:00:00","2010-09-27T00:00:00","2010-09-28T00:00:00","2010-09-29T00:00:00","2010-09-30T00:00:00","2010-10-01T00:00:00","2010-10-04T00:00:00","2010-10-05T00:00:00","2010-10-06T00:00:00","2010-10-07T00:00:00","2010-10-08T00:00:00","2010-10-11T00:00:00","2010-10-12T00:00:00","2010-10-13T00:00:00","2010-10-14T00:00:00","2010-10-15T00:00:00","2010-10-18T00:00:00","2010-10-19T00:00:00","2010-10-20T00:00:00","2010-10-21T00:00:00","2010-10-22T00:00:00","2010-10-25T00:00:00","2010-10-26T00:00:00","2010-10-27T00:00:00","2010-10-28T00:00:00","2010-10-29T00:00:00","2010-11-01T00:00:00","2010-11-02T00:00:00","2010-11-03T00:00:00","2010-11-04T00:00:00","2010-11-05T00:00:00","2010-11-08T00:00:00","2010-11-09T00:00:00","2010-11-10T00:00:00","2010-11-11T00:00:00","2010-11-12T00:00:00","2010-11-15T00:00:00","2010-11-16T00:00:00","2010-11-17T00:00:00","2010-11-18T00:00:00","2010-11-19T00:00:00","2010-11-22T00:00:00","2010-11-23T00:00:00","2010-11-24T00:00:00","2010-11-26T00:00:00","2010-11-29T00:00:00","2010-11-30T00:00:00","2010-12-01T00:00:00","2010-12-02T00:00:00","2010-12-03T00:00:00","2010-12-06T00:00:00","2010-12-07T00:00:00","2010-12-08T00:00:00","2010-12-09T00:00:00","2010-12-10T00:00:00","2010-12-13T00:00:00","2010-12-14T00:00:00","2010-12-15T00:00:00","2010-12-16T00:00:00","2010-12-17T00:00:00","2010-12-20T00:00:00","2010-12-21T00:00:00","2010-12-22T00:00:00","2010-12-23T00:00:00","2010-12-27T00:00:00","2010-12-28T00:00:00","2010-12-29T00:00:00","2010-12-30T00:00:00","2010-12-31T00:00:00","2011-01-03T00:00:00","2011-01-04T00:00:00","2011-01-05T00:00:00","2011-01-06T00:00:00","2011-01-07T00:00:00","2011-01-10T00:00:00","2011-01-11T00:00:00","2011-01-12T00:00:00","2011-01-13T00:00:00","2011-01-14T00:00:00","2011-01-18T00:00:00","2011-01-19T00:00:00","2011-01-20T00:00:00","2011-01-21T00:00:00","2011-01-24T00:00:00","2011-01-25T00:00:00","2011-01-26T00:00:00","2011-01-27T00:00:00","2011-01-28T00:00:00","2011-01-31T00:00:00","2011-02-01T00:00:00","2011-02-02T00:00:00","2011-02-03T00:00:00","2011-02-04T00:00:00","2011-02-07T00:00:00","2011-02-08T00:00:00","2011-02-09T00:00:00","2011-02-10T00:00:00","2011-02-11T00:00:00","2011-02-14T00:00:00","2011-02-15T00:00:00","2011-02-16T00:00:00","2011-02-17T00:00:00","2011-02-18T00:00:00","2011-02-22T00:00:00","2011-02-23T00:00:00","2011-02-24T00:00:00","2011-02-25T00:00:00","2011-02-28T00:00:00","2011-03-01T00:00:00","2011-03-02T00:00:00","2011-03-03T00:00:00","2011-03-04T00:00:00","2011-03-07T00:00:00","2011-03-08T00:00:00","2011-03-09T00:00:00","2011-03-10T00:00:00","2011-03-11T00:00:00","2011-03-14T00:00:00","2011-03-15T00:00:00","2011-03-16T00:00:00","2011-03-17T00:00:00","2011-03-18T00:00:00","2011-03-21T00:00:00","2011-03-22T00:00:00","2011-03-23T00:00:00","2011-03-24T00:00:00","2011-03-25T00:00:00","2011-03-28T00:00:00","2011-03-29T00:00:00","2011-03-30T00:00:00","2011-03-31T00:00:00","2011-04-01T00:00:00","2011-04-04T00:00:00","2011-04-05T00:00:00","2011-04-06T00:00:00","2011-04-07T00:00:00","2011-04-08T00:00:00","2011-04-11T00:00:00","2011-04-12T00:00:00","2011-04-13T00:00:00","2011-04-14T00:00:00","2011-04-15T00:00:00","2011-04-18T00:00:00","2011-04-19T00:00:00","2011-04-20T00:00:00","2011-04-21T00:00:00","2011-04-25T00:00:00","2011-04-26T00:00:00","2011-04-27T00:00:00","2011-04-28T00:00:00","2011-04-29T00:00:00","2011-05-02T00:00:00","2011-05-03T00:00:00","2011-05-04T00:00:00","2011-05-05T00:00:00","2011-05-06T00:00:00","2011-05-09T00:00:00","2011-05-10T00:00:00","2011-05-11T00:00:00","2011-05-12T00:00:00","2011-05-13T00:00:00","2011-05-16T00:00:00","2011-05-17T00:00:00","2011-05-18T00:00:00","2011-05-19T00:00:00","2011-05-20T00:00:00","2011-05-23T00:00:00","2011-05-24T00:00:00","2011-05-25T00:00:00","2011-05-26T00:00:00","2011-05-27T00:00:00","2011-05-31T00:00:00","2011-06-01T00:00:00","2011-06-02T00:00:00","2011-06-03T00:00:00","2011-06-06T00:00:00","2011-06-07T00:00:00","2011-06-08T00:00:00","2011-06-09T00:00:00","2011-06-10T00:00:00","2011-06-13T00:00:00","2011-06-14T00:00:00","2011-06-15T00:00:00","2011-06-16T00:00:00","2011-06-17T00:00:00","2011-06-20T00:00:00","2011-06-21T00:00:00","2011-06-22T00:00:00","2011-06-23T00:00:00","2011-06-24T00:00:00","2011-06-27T00:00:00","2011-06-28T00:00:00","2011-06-29T00:00:00","2011-06-30T00:00:00","2011-07-01T00:00:00","2011-07-05T00:00:00","2011-07-06T00:00:00","2011-07-07T00:00:00","2011-07-08T00:00:00","2011-07-11T00:00:00","2011-07-12T00:00:00","2011-07-13T00:00:00","2011-07-14T00:00:00","2011-07-15T00:00:00","2011-07-18T00:00:00","2011-07-19T00:00:00","2011-07-20T00:00:00","2011-07-21T00:00:00","2011-07-22T00:00:00","2011-07-25T00:00:00","2011-07-26T00:00:00","2011-07-27T00:00:00","2011-07-28T00:00:00","2011-07-29T00:00:00","2011-08-01T00:00:00","2011-08-02T00:00:00","2011-08-03T00:00:00","2011-08-04T00:00:00","2011-08-05T00:00:00","2011-08-08T00:00:00","2011-08-09T00:00:00","2011-08-10T00:00:00","2011-08-11T00:00:00","2011-08-12T00:00:00","2011-08-15T00:00:00","2011-08-16T00:00:00","2011-08-17T00:00:00","2011-08-18T00:00:00","2011-08-19T00:00:00","2011-08-22T00:00:00","2011-08-23T00:00:00","2011-08-24T00:00:00","2011-08-25T00:00:00","2011-08-26T00:00:00","2011-08-29T00:00:00","2011-08-30T00:00:00","2011-08-31T00:00:00","2011-09-01T00:00:00","2011-09-02T00:00:00","2011-09-06T00:00:00","2011-09-07T00:00:00","2011-09-08T00:00:00","2011-09-09T00:00:00","2011-09-12T00:00:00","2011-09-13T00:00:00","2011-09-14T00:00:00","2011-09-15T00:00:00","2011-09-16T00:00:00","2011-09-19T00:00:00","2011-09-20T00:00:00","2011-09-21T00:00:00","2011-09-22T00:00:00","2011-09-23T00:00:00","2011-09-26T00:00:00","2011-09-27T00:00:00","2011-09-28T00:00:00","2011-09-29T00:00:00","2011-09-30T00:00:00","2011-10-03T00:00:00","2011-10-04T00:00:00","2011-10-05T00:00:00","2011-10-06T00:00:00","2011-10-07T00:00:00","2011-10-10T00:00:00","2011-10-11T00:00:00","2011-10-12T00:00:00","2011-10-13T00:00:00","2011-10-14T00:00:00","2011-10-17T00:00:00","2011-10-18T00:00:00","2011-10-19T00:00:00","2011-10-20T00:00:00","2011-10-21T00:00:00","2011-10-24T00:00:00","2011-10-25T00:00:00","2011-10-26T00:00:00","2011-10-27T00:00:00","2011-10-28T00:00:00","2011-10-31T00:00:00","2011-11-01T00:00:00","2011-11-02T00:00:00","2011-11-03T00:00:00","2011-11-04T00:00:00","2011-11-07T00:00:00","2011-11-08T00:00:00","2011-11-09T00:00:00","2011-11-10T00:00:00","2011-11-11T00:00:00","2011-11-14T00:00:00","2011-11-15T00:00:00","2011-11-16T00:00:00","2011-11-17T00:00:00","2011-11-18T00:00:00","2011-11-21T00:00:00","2011-11-22T00:00:00","2011-11-23T00:00:00","2011-11-25T00:00:00","2011-11-28T00:00:00","2011-11-29T00:00:00","2011-11-30T00:00:00","2011-12-01T00:00:00","2011-12-02T00:00:00","2011-12-05T00:00:00","2011-12-06T00:00:00","2011-12-07T00:00:00","2011-12-08T00:00:00","2011-12-09T00:00:00","2011-12-12T00:00:00","2011-12-13T00:00:00","2011-12-14T00:00:00","2011-12-15T00:00:00","2011-12-16T00:00:00","2011-12-19T00:00:00","2011-12-20T00:00:00","2011-12-21T00:00:00","2011-12-22T00:00:00","2011-12-23T00:00:00","2011-12-27T00:00:00","2011-12-28T00:00:00","2011-12-29T00:00:00","2011-12-30T00:00:00","2012-01-03T00:00:00","2012-01-04T00:00:00","2012-01-05T00:00:00","2012-01-06T00:00:00","2012-01-09T00:00:00","2012-01-10T00:00:00","2012-01-11T00:00:00","2012-01-12T00:00:00","2012-01-13T00:00:00","2012-01-17T00:00:00","2012-01-18T00:00:00","2012-01-19T00:00:00","2012-01-20T00:00:00","2012-01-23T00:00:00","2012-01-24T00:00:00","2012-01-25T00:00:00","2012-01-26T00:00:00","2012-01-27T00:00:00","2012-01-30T00:00:00","2012-01-31T00:00:00","2012-02-01T00:00:00","2012-02-02T00:00:00","2012-02-03T00:00:00","2012-02-06T00:00:00","2012-02-07T00:00:00","2012-02-08T00:00:00","2012-02-09T00:00:00","2012-02-10T00:00:00","2012-02-13T00:00:00","2012-02-14T00:00:00","2012-02-15T00:00:00","2012-02-16T00:00:00","2012-02-17T00:00:00","2012-02-21T00:00:00","2012-02-22T00:00:00","2012-02-23T00:00:00","2012-02-24T00:00:00","2012-02-27T00:00:00","2012-02-28T00:00:00","2012-02-29T00:00:00","2012-03-01T00:00:00","2012-03-02T00:00:00","2012-03-05T00:00:00","2012-03-06T00:00:00","2012-03-07T00:00:00","2012-03-08T00:00:00","2012-03-09T00:00:00","2012-03-12T00:00:00","2012-03-13T00:00:00","2012-03-14T00:00:00","2012-03-15T00:00:00","2012-03-16T00:00:00","2012-03-19T00:00:00","2012-03-20T00:00:00","2012-03-21T00:00:00","2012-03-22T00:00:00","2012-03-23T00:00:00","2012-03-26T00:00:00","2012-03-27T00:00:00","2012-03-28T00:00:00","2012-03-29T00:00:00","2012-03-30T00:00:00","2012-04-02T00:00:00","2012-04-03T00:00:00","2012-04-04T00:00:00","2012-04-05T00:00:00","2012-04-09T00:00:00","2012-04-10T00:00:00","2012-04-11T00:00:00","2012-04-12T00:00:00","2012-04-13T00:00:00","2012-04-16T00:00:00","2012-04-17T00:00:00","2012-04-18T00:00:00","2012-04-19T00:00:00","2012-04-20T00:00:00","2012-04-23T00:00:00","2012-04-24T00:00:00","2012-04-25T00:00:00","2012-04-26T00:00:00","2012-04-27T00:00:00","2012-04-30T00:00:00","2012-05-01T00:00:00","2012-05-02T00:00:00","2012-05-03T00:00:00","2012-05-04T00:00:00","2012-05-07T00:00:00","2012-05-08T00:00:00","2012-05-09T00:00:00","2012-05-10T00:00:00","2012-05-11T00:00:00","2012-05-14T00:00:00","2012-05-15T00:00:00","2012-05-16T00:00:00","2012-05-17T00:00:00","2012-05-18T00:00:00","2012-05-21T00:00:00","2012-05-22T00:00:00","2012-05-23T00:00:00","2012-05-24T00:00:00","2012-05-25T00:00:00","2012-05-29T00:00:00","2012-05-30T00:00:00","2012-05-31T00:00:00","2012-06-01T00:00:00","2012-06-04T00:00:00","2012-06-05T00:00:00","2012-06-06T00:00:00","2012-06-07T00:00:00","2012-06-08T00:00:00","2012-06-11T00:00:00","2012-06-12T00:00:00","2012-06-13T00:00:00","2012-06-14T00:00:00","2012-06-15T00:00:00","2012-06-18T00:00:00","2012-06-19T00:00:00","2012-06-20T00:00:00","2012-06-21T00:00:00","2012-06-22T00:00:00","2012-06-25T00:00:00","2012-06-26T00:00:00","2012-06-27T00:00:00","2012-06-28T00:00:00","2012-06-29T00:00:00","2012-07-02T00:00:00","2012-07-03T00:00:00","2012-07-05T00:00:00","2012-07-06T00:00:00","2012-07-09T00:00:00","2012-07-10T00:00:00","2012-07-11T00:00:00","2012-07-12T00:00:00","2012-07-13T00:00:00","2012-07-16T00:00:00","2012-07-17T00:00:00","2012-07-18T00:00:00","2012-07-19T00:00:00","2012-07-20T00:00:00","2012-07-23T00:00:00","2012-07-24T00:00:00","2012-07-25T00:00:00","2012-07-26T00:00:00","2012-07-27T00:00:00","2012-07-30T00:00:00","2012-07-31T00:00:00","2012-08-01T00:00:00","2012-08-02T00:00:00","2012-08-03T00:00:00","2012-08-06T00:00:00","2012-08-07T00:00:00","2012-08-08T00:00:00","2012-08-09T00:00:00","2012-08-10T00:00:00","2012-08-13T00:00:00","2012-08-14T00:00:00","2012-08-15T00:00:00","2012-08-16T00:00:00","2012-08-17T00:00:00","2012-08-20T00:00:00","2012-08-21T00:00:00","2012-08-22T00:00:00","2012-08-23T00:00:00","2012-08-24T00:00:00","2012-08-27T00:00:00","2012-08-28T00:00:00","2012-08-29T00:00:00","2012-08-30T00:00:00","2012-08-31T00:00:00","2012-09-04T00:00:00","2012-09-05T00:00:00","2012-09-06T00:00:00","2012-09-07T00:00:00","2012-09-10T00:00:00","2012-09-11T00:00:00","2012-09-12T00:00:00","2012-09-13T00:00:00","2012-09-14T00:00:00","2012-09-17T00:00:00","2012-09-18T00:00:00","2012-09-19T00:00:00","2012-09-20T00:00:00","2012-09-21T00:00:00","2012-09-24T00:00:00","2012-09-25T00:00:00","2012-09-26T00:00:00","2012-09-27T00:00:00","2012-09-28T00:00:00","2012-10-01T00:00:00","2012-10-02T00:00:00","2012-10-03T00:00:00","2012-10-04T00:00:00","2012-10-05T00:00:00","2012-10-08T00:00:00","2012-10-09T00:00:00","2012-10-10T00:00:00","2012-10-11T00:00:00","2012-10-12T00:00:00","2012-10-15T00:00:00","2012-10-16T00:00:00","2012-10-17T00:00:00","2012-10-18T00:00:00","2012-10-19T00:00:00","2012-10-22T00:00:00","2012-10-23T00:00:00","2012-10-24T00:00:00","2012-10-25T00:00:00","2012-10-26T00:00:00","2012-10-31T00:00:00","2012-11-01T00:00:00","2012-11-02T00:00:00","2012-11-05T00:00:00","2012-11-06T00:00:00","2012-11-07T00:00:00","2012-11-08T00:00:00","2012-11-09T00:00:00","2012-11-12T00:00:00","2012-11-13T00:00:00","2012-11-14T00:00:00","2012-11-15T00:00:00","2012-11-16T00:00:00","2012-11-19T00:00:00","2012-11-20T00:00:00","2012-11-21T00:00:00","2012-11-23T00:00:00","2012-11-26T00:00:00","2012-11-27T00:00:00","2012-11-28T00:00:00","2012-11-29T00:00:00","2012-11-30T00:00:00","2012-12-03T00:00:00","2012-12-04T00:00:00","2012-12-05T00:00:00","2012-12-06T00:00:00","2012-12-07T00:00:00","2012-12-10T00:00:00","2012-12-11T00:00:00","2012-12-12T00:00:00","2012-12-13T00:00:00","2012-12-14T00:00:00","2012-12-17T00:00:00","2012-12-18T00:00:00","2012-12-19T00:00:00","2012-12-20T00:00:00","2012-12-21T00:00:00","2012-12-24T00:00:00","2012-12-26T00:00:00","2012-12-27T00:00:00","2012-12-28T00:00:00","2012-12-31T00:00:00","2013-01-02T00:00:00","2013-01-03T00:00:00","2013-01-04T00:00:00","2013-01-07T00:00:00","2013-01-08T00:00:00","2013-01-09T00:00:00","2013-01-10T00:00:00","2013-01-11T00:00:00","2013-01-14T00:00:00","2013-01-15T00:00:00","2013-01-16T00:00:00","2013-01-17T00:00:00","2013-01-18T00:00:00","2013-01-22T00:00:00","2013-01-23T00:00:00","2013-01-24T00:00:00","2013-01-25T00:00:00","2013-01-28T00:00:00","2013-01-29T00:00:00","2013-01-30T00:00:00","2013-01-31T00:00:00","2013-02-01T00:00:00","2013-02-04T00:00:00","2013-02-05T00:00:00","2013-02-06T00:00:00","2013-02-07T00:00:00","2013-02-08T00:00:00","2013-02-11T00:00:00","2013-02-12T00:00:00","2013-02-13T00:00:00","2013-02-14T00:00:00","2013-02-15T00:00:00","2013-02-19T00:00:00","2013-02-20T00:00:00","2013-02-21T00:00:00","2013-02-22T00:00:00","2013-02-25T00:00:00","2013-02-26T00:00:00","2013-02-27T00:00:00","2013-02-28T00:00:00","2013-03-01T00:00:00","2013-03-04T00:00:00","2013-03-05T00:00:00","2013-03-06T00:00:00","2013-03-07T00:00:00","2013-03-08T00:00:00","2013-03-11T00:00:00","2013-03-12T00:00:00","2013-03-13T00:00:00","2013-03-14T00:00:00","2013-03-15T00:00:00","2013-03-18T00:00:00","2013-03-19T00:00:00","2013-03-20T00:00:00","2013-03-21T00:00:00","2013-03-22T00:00:00","2013-03-25T00:00:00","2013-03-26T00:00:00","2013-03-27T00:00:00","2013-03-28T00:00:00","2013-04-01T00:00:00","2013-04-02T00:00:00","2013-04-03T00:00:00","2013-04-04T00:00:00","2013-04-05T00:00:00","2013-04-08T00:00:00","2013-04-09T00:00:00","2013-04-10T00:00:00","2013-04-11T00:00:00","2013-04-12T00:00:00","2013-04-15T00:00:00","2013-04-16T00:00:00","2013-04-17T00:00:00","2013-04-18T00:00:00","2013-04-19T00:00:00","2013-04-22T00:00:00","2013-04-23T00:00:00","2013-04-24T00:00:00","2013-04-25T00:00:00","2013-04-26T00:00:00","2013-04-29T00:00:00","2013-04-30T00:00:00","2013-05-01T00:00:00","2013-05-02T00:00:00","2013-05-03T00:00:00","2013-05-06T00:00:00","2013-05-07T00:00:00","2013-05-08T00:00:00","2013-05-09T00:00:00","2013-05-10T00:00:00","2013-05-13T00:00:00","2013-05-14T00:00:00","2013-05-15T00:00:00","2013-05-16T00:00:00","2013-05-17T00:00:00","2013-05-20T00:00:00","2013-05-21T00:00:00","2013-05-22T00:00:00","2013-05-23T00:00:00","2013-05-24T00:00:00","2013-05-28T00:00:00","2013-05-29T00:00:00","2013-05-30T00:00:00","2013-05-31T00:00:00","2013-06-03T00:00:00","2013-06-04T00:00:00","2013-06-05T00:00:00","2013-06-06T00:00:00","2013-06-07T00:00:00","2013-06-10T00:00:00","2013-06-11T00:00:00","2013-06-12T00:00:00","2013-06-13T00:00:00","2013-06-14T00:00:00","2013-06-17T00:00:00","2013-06-18T00:00:00","2013-06-19T00:00:00","2013-06-20T00:00:00","2013-06-21T00:00:00","2013-06-24T00:00:00","2013-06-25T00:00:00","2013-06-26T00:00:00","2013-06-27T00:00:00","2013-06-28T00:00:00","2013-07-01T00:00:00","2013-07-02T00:00:00","2013-07-03T00:00:00","2013-07-05T00:00:00","2013-07-08T00:00:00","2013-07-09T00:00:00","2013-07-10T00:00:00","2013-07-11T00:00:00","2013-07-12T00:00:00","2013-07-15T00:00:00","2013-07-16T00:00:00","2013-07-17T00:00:00","2013-07-18T00:00:00","2013-07-19T00:00:00","2013-07-22T00:00:00","2013-07-23T00:00:00","2013-07-24T00:00:00","2013-07-25T00:00:00","2013-07-26T00:00:00","2013-07-29T00:00:00","2013-07-30T00:00:00","2013-07-31T00:00:00","2013-08-01T00:00:00","2013-08-02T00:00:00","2013-08-05T00:00:00","2013-08-06T00:00:00","2013-08-07T00:00:00","2013-08-08T00:00:00","2013-08-09T00:00:00","2013-08-12T00:00:00","2013-08-13T00:00:00","2013-08-14T00:00:00","2013-08-15T00:00:00","2013-08-16T00:00:00","2013-08-19T00:00:00","2013-08-20T00:00:00","2013-08-21T00:00:00","2013-08-22T00:00:00","2013-08-23T00:00:00","2013-08-26T00:00:00","2013-08-27T00:00:00","2013-08-28T00:00:00","2013-08-29T00:00:00","2013-08-30T00:00:00","2013-09-03T00:00:00","2013-09-04T00:00:00","2013-09-05T00:00:00","2013-09-06T00:00:00","2013-09-09T00:00:00","2013-09-10T00:00:00","2013-09-11T00:00:00","2013-09-12T00:00:00","2013-09-13T00:00:00","2013-09-16T00:00:00","2013-09-17T00:00:00","2013-09-18T00:00:00","2013-09-19T00:00:00","2013-09-20T00:00:00","2013-09-23T00:00:00","2013-09-24T00:00:00","2013-09-25T00:00:00","2013-09-26T00:00:00","2013-09-27T00:00:00","2013-09-30T00:00:00","2013-10-01T00:00:00","2013-10-02T00:00:00","2013-10-03T00:00:00","2013-10-04T00:00:00","2013-10-07T00:00:00","2013-10-08T00:00:00","2013-10-09T00:00:00","2013-10-10T00:00:00","2013-10-11T00:00:00","2013-10-14T00:00:00","2013-10-15T00:00:00","2013-10-16T00:00:00","2013-10-17T00:00:00","2013-10-18T00:00:00","2013-10-21T00:00:00","2013-10-22T00:00:00","2013-10-23T00:00:00","2013-10-24T00:00:00","2013-10-25T00:00:00","2013-10-28T00:00:00","2013-10-29T00:00:00","2013-10-30T00:00:00","2013-10-31T00:00:00","2013-11-01T00:00:00","2013-11-04T00:00:00","2013-11-05T00:00:00","2013-11-06T00:00:00","2013-11-07T00:00:00","2013-11-08T00:00:00","2013-11-11T00:00:00","2013-11-12T00:00:00","2013-11-13T00:00:00","2013-11-14T00:00:00","2013-11-15T00:00:00","2013-11-18T00:00:00","2013-11-19T00:00:00","2013-11-20T00:00:00","2013-11-21T00:00:00","2013-11-22T00:00:00","2013-11-25T00:00:00","2013-11-26T00:00:00","2013-11-27T00:00:00","2013-11-29T00:00:00","2013-12-02T00:00:00","2013-12-03T00:00:00","2013-12-04T00:00:00","2013-12-05T00:00:00","2013-12-06T00:00:00","2013-12-09T00:00:00","2013-12-10T00:00:00","2013-12-11T00:00:00","2013-12-12T00:00:00","2013-12-13T00:00:00","2013-12-16T00:00:00","2013-12-17T00:00:00","2013-12-18T00:00:00","2013-12-19T00:00:00","2013-12-20T00:00:00","2013-12-23T00:00:00","2013-12-24T00:00:00","2013-12-26T00:00:00","2013-12-27T00:00:00","2013-12-30T00:00:00","2013-12-31T00:00:00","2014-01-02T00:00:00","2014-01-03T00:00:00","2014-01-06T00:00:00","2014-01-07T00:00:00","2014-01-08T00:00:00","2014-01-09T00:00:00","2014-01-10T00:00:00","2014-01-13T00:00:00","2014-01-14T00:00:00","2014-01-15T00:00:00","2014-01-16T00:00:00","2014-01-17T00:00:00","2014-01-21T00:00:00","2014-01-22T00:00:00","2014-01-23T00:00:00","2014-01-24T00:00:00","2014-01-27T00:00:00","2014-01-28T00:00:00","2014-01-29T00:00:00","2014-01-30T00:00:00","2014-01-31T00:00:00","2014-02-03T00:00:00","2014-02-04T00:00:00","2014-02-05T00:00:00","2014-02-06T00:00:00","2014-02-07T00:00:00","2014-02-10T00:00:00","2014-02-11T00:00:00","2014-02-12T00:00:00","2014-02-13T00:00:00","2014-02-14T00:00:00","2014-02-18T00:00:00","2014-02-19T00:00:00","2014-02-20T00:00:00","2014-02-21T00:00:00","2014-02-24T00:00:00","2014-02-25T00:00:00","2014-02-26T00:00:00","2014-02-27T00:00:00","2014-02-28T00:00:00","2014-03-03T00:00:00","2014-03-04T00:00:00","2014-03-05T00:00:00","2014-03-06T00:00:00","2014-03-07T00:00:00","2014-03-10T00:00:00","2014-03-11T00:00:00","2014-03-12T00:00:00","2014-03-13T00:00:00","2014-03-14T00:00:00","2014-03-17T00:00:00","2014-03-18T00:00:00","2014-03-19T00:00:00","2014-03-20T00:00:00","2014-03-21T00:00:00","2014-03-24T00:00:00","2014-03-25T00:00:00","2014-03-26T00:00:00","2014-03-27T00:00:00","2014-03-28T00:00:00","2014-03-31T00:00:00","2014-04-01T00:00:00","2014-04-02T00:00:00","2014-04-03T00:00:00","2014-04-04T00:00:00","2014-04-07T00:00:00","2014-04-08T00:00:00","2014-04-09T00:00:00","2014-04-10T00:00:00","2014-04-11T00:00:00","2014-04-14T00:00:00","2014-04-15T00:00:00","2014-04-16T00:00:00","2014-04-17T00:00:00","2014-04-21T00:00:00","2014-04-22T00:00:00","2014-04-23T00:00:00","2014-04-24T00:00:00","2014-04-25T00:00:00","2014-04-28T00:00:00","2014-04-29T00:00:00","2014-04-30T00:00:00","2014-05-01T00:00:00","2014-05-02T00:00:00","2014-05-05T00:00:00","2014-05-06T00:00:00","2014-05-07T00:00:00","2014-05-08T00:00:00","2014-05-09T00:00:00","2014-05-12T00:00:00","2014-05-13T00:00:00","2014-05-14T00:00:00","2014-05-15T00:00:00","2014-05-16T00:00:00","2014-05-19T00:00:00","2014-05-20T00:00:00","2014-05-21T00:00:00","2014-05-22T00:00:00","2014-05-23T00:00:00","2014-05-27T00:00:00","2014-05-28T00:00:00","2014-05-29T00:00:00","2014-05-30T00:00:00","2014-06-02T00:00:00","2014-06-03T00:00:00","2014-06-04T00:00:00","2014-06-05T00:00:00","2014-06-06T00:00:00","2014-06-09T00:00:00","2014-06-10T00:00:00","2014-06-11T00:00:00","2014-06-12T00:00:00","2014-06-13T00:00:00","2014-06-16T00:00:00","2014-06-17T00:00:00","2014-06-18T00:00:00","2014-06-19T00:00:00","2014-06-20T00:00:00","2014-06-23T00:00:00","2014-06-24T00:00:00","2014-06-25T00:00:00","2014-06-26T00:00:00","2014-06-27T00:00:00","2014-06-30T00:00:00","2014-07-01T00:00:00","2014-07-02T00:00:00","2014-07-03T00:00:00","2014-07-07T00:00:00","2014-07-08T00:00:00","2014-07-09T00:00:00","2014-07-10T00:00:00","2014-07-11T00:00:00","2014-07-14T00:00:00","2014-07-15T00:00:00","2014-07-16T00:00:00","2014-07-17T00:00:00","2014-07-18T00:00:00","2014-07-21T00:00:00","2014-07-22T00:00:00","2014-07-23T00:00:00","2014-07-24T00:00:00","2014-07-25T00:00:00","2014-07-28T00:00:00","2014-07-29T00:00:00","2014-07-30T00:00:00","2014-07-31T00:00:00","2014-08-01T00:00:00","2014-08-04T00:00:00","2014-08-05T00:00:00","2014-08-06T00:00:00","2014-08-07T00:00:00","2014-08-08T00:00:00","2014-08-11T00:00:00","2014-08-12T00:00:00","2014-08-13T00:00:00","2014-08-14T00:00:00","2014-08-15T00:00:00","2014-08-18T00:00:00","2014-08-19T00:00:00","2014-08-20T00:00:00","2014-08-21T00:00:00","2014-08-22T00:00:00","2014-08-25T00:00:00","2014-08-26T00:00:00","2014-08-27T00:00:00","2014-08-28T00:00:00","2014-08-29T00:00:00","2014-09-02T00:00:00","2014-09-03T00:00:00","2014-09-04T00:00:00","2014-09-05T00:00:00","2014-09-08T00:00:00","2014-09-09T00:00:00","2014-09-10T00:00:00","2014-09-11T00:00:00","2014-09-12T00:00:00","2014-09-15T00:00:00","2014-09-16T00:00:00","2014-09-17T00:00:00","2014-09-18T00:00:00","2014-09-19T00:00:00","2014-09-22T00:00:00","2014-09-23T00:00:00","2014-09-24T00:00:00","2014-09-25T00:00:00","2014-09-26T00:00:00","2014-09-29T00:00:00","2014-09-30T00:00:00","2014-10-01T00:00:00","2014-10-02T00:00:00","2014-10-03T00:00:00","2014-10-06T00:00:00","2014-10-07T00:00:00","2014-10-08T00:00:00","2014-10-09T00:00:00","2014-10-10T00:00:00","2014-10-13T00:00:00","2014-10-14T00:00:00","2014-10-15T00:00:00","2014-10-16T00:00:00","2014-10-17T00:00:00","2014-10-20T00:00:00","2014-10-21T00:00:00","2014-10-22T00:00:00","2014-10-23T00:00:00","2014-10-24T00:00:00","2014-10-27T00:00:00","2014-10-28T00:00:00","2014-10-29T00:00:00","2014-10-30T00:00:00","2014-10-31T00:00:00","2014-11-03T00:00:00","2014-11-04T00:00:00","2014-11-05T00:00:00","2014-11-06T00:00:00","2014-11-07T00:00:00","2014-11-10T00:00:00","2014-11-11T00:00:00","2014-11-12T00:00:00","2014-11-13T00:00:00","2014-11-14T00:00:00","2014-11-17T00:00:00","2014-11-18T00:00:00","2014-11-19T00:00:00","2014-11-20T00:00:00","2014-11-21T00:00:00","2014-11-24T00:00:00","2014-11-25T00:00:00","2014-11-26T00:00:00","2014-11-28T00:00:00","2014-12-01T00:00:00","2014-12-02T00:00:00","2014-12-03T00:00:00","2014-12-04T00:00:00","2014-12-05T00:00:00","2014-12-08T00:00:00","2014-12-09T00:00:00","2014-12-10T00:00:00","2014-12-11T00:00:00","2014-12-12T00:00:00","2014-12-15T00:00:00","2014-12-16T00:00:00","2014-12-17T00:00:00","2014-12-18T00:00:00","2014-12-19T00:00:00","2014-12-22T00:00:00","2014-12-23T00:00:00","2014-12-24T00:00:00","2014-12-26T00:00:00","2014-12-29T00:00:00","2014-12-30T00:00:00","2014-12-31T00:00:00","2015-01-02T00:00:00","2015-01-05T00:00:00","2015-01-06T00:00:00","2015-01-07T00:00:00","2015-01-08T00:00:00","2015-01-09T00:00:00","2015-01-12T00:00:00","2015-01-13T00:00:00","2015-01-14T00:00:00","2015-01-15T00:00:00","2015-01-16T00:00:00","2015-01-20T00:00:00","2015-01-21T00:00:00","2015-01-22T00:00:00","2015-01-23T00:00:00","2015-01-26T00:00:00","2015-01-27T00:00:00","2015-01-28T00:00:00","2015-01-29T00:00:00","2015-01-30T00:00:00","2015-02-02T00:00:00","2015-02-03T00:00:00","2015-02-04T00:00:00","2015-02-05T00:00:00","2015-02-06T00:00:00","2015-02-09T00:00:00","2015-02-10T00:00:00","2015-02-11T00:00:00","2015-02-12T00:00:00","2015-02-13T00:00:00","2015-02-17T00:00:00","2015-02-18T00:00:00","2015-02-19T00:00:00","2015-02-20T00:00:00","2015-02-23T00:00:00","2015-02-24T00:00:00","2015-02-25T00:00:00","2015-02-26T00:00:00","2015-02-27T00:00:00","2015-03-02T00:00:00","2015-03-03T00:00:00","2015-03-04T00:00:00","2015-03-05T00:00:00","2015-03-06T00:00:00","2015-03-09T00:00:00","2015-03-10T00:00:00","2015-03-11T00:00:00","2015-03-12T00:00:00","2015-03-13T00:00:00","2015-03-16T00:00:00","2015-03-17T00:00:00","2015-03-18T00:00:00","2015-03-19T00:00:00","2015-03-20T00:00:00","2015-03-23T00:00:00","2015-03-24T00:00:00","2015-03-25T00:00:00","2015-03-26T00:00:00","2015-03-27T00:00:00","2015-03-30T00:00:00","2015-03-31T00:00:00","2015-04-01T00:00:00","2015-04-02T00:00:00","2015-04-06T00:00:00","2015-04-07T00:00:00","2015-04-08T00:00:00","2015-04-09T00:00:00","2015-04-10T00:00:00","2015-04-13T00:00:00","2015-04-14T00:00:00","2015-04-15T00:00:00","2015-04-16T00:00:00","2015-04-17T00:00:00","2015-04-20T00:00:00","2015-04-21T00:00:00","2015-04-22T00:00:00","2015-04-23T00:00:00","2015-04-24T00:00:00","2015-04-27T00:00:00","2015-04-28T00:00:00","2015-04-29T00:00:00","2015-04-30T00:00:00","2015-05-01T00:00:00","2015-05-04T00:00:00","2015-05-05T00:00:00","2015-05-06T00:00:00","2015-05-07T00:00:00","2015-05-08T00:00:00","2015-05-11T00:00:00","2015-05-12T00:00:00","2015-05-13T00:00:00","2015-05-14T00:00:00","2015-05-15T00:00:00","2015-05-18T00:00:00","2015-05-19T00:00:00","2015-05-20T00:00:00","2015-05-21T00:00:00","2015-05-22T00:00:00","2015-05-26T00:00:00","2015-05-27T00:00:00","2015-05-28T00:00:00","2015-05-29T00:00:00","2015-06-01T00:00:00","2015-06-02T00:00:00","2015-06-03T00:00:00","2015-06-04T00:00:00","2015-06-05T00:00:00","2015-06-08T00:00:00","2015-06-09T00:00:00","2015-06-10T00:00:00","2015-06-11T00:00:00","2015-06-12T00:00:00","2015-06-15T00:00:00","2015-06-16T00:00:00","2015-06-17T00:00:00","2015-06-18T00:00:00","2015-06-19T00:00:00","2015-06-22T00:00:00","2015-06-23T00:00:00","2015-06-24T00:00:00","2015-06-25T00:00:00","2015-06-26T00:00:00","2015-06-29T00:00:00","2015-06-30T00:00:00","2015-07-01T00:00:00","2015-07-02T00:00:00","2015-07-06T00:00:00","2015-07-07T00:00:00","2015-07-08T00:00:00","2015-07-09T00:00:00","2015-07-10T00:00:00","2015-07-13T00:00:00","2015-07-14T00:00:00","2015-07-15T00:00:00","2015-07-16T00:00:00","2015-07-17T00:00:00","2015-07-20T00:00:00","2015-07-21T00:00:00","2015-07-22T00:00:00","2015-07-23T00:00:00","2015-07-24T00:00:00","2015-07-27T00:00:00","2015-07-28T00:00:00","2015-07-29T00:00:00","2015-07-30T00:00:00","2015-07-31T00:00:00","2015-08-03T00:00:00","2015-08-04T00:00:00","2015-08-05T00:00:00","2015-08-06T00:00:00","2015-08-07T00:00:00","2015-08-10T00:00:00","2015-08-11T00:00:00","2015-08-12T00:00:00","2015-08-13T00:00:00","2015-08-14T00:00:00","2015-08-17T00:00:00","2015-08-18T00:00:00","2015-08-19T00:00:00","2015-08-20T00:00:00","2015-08-21T00:00:00","2015-08-24T00:00:00","2015-08-25T00:00:00","2015-08-26T00:00:00","2015-08-27T00:00:00","2015-08-28T00:00:00","2015-08-31T00:00:00","2015-09-01T00:00:00","2015-09-02T00:00:00","2015-09-03T00:00:00","2015-09-04T00:00:00","2015-09-08T00:00:00","2015-09-09T00:00:00","2015-09-10T00:00:00","2015-09-11T00:00:00","2015-09-14T00:00:00","2015-09-15T00:00:00","2015-09-16T00:00:00","2015-09-17T00:00:00","2015-09-18T00:00:00","2015-09-21T00:00:00","2015-09-22T00:00:00","2015-09-23T00:00:00","2015-09-24T00:00:00","2015-09-25T00:00:00","2015-09-28T00:00:00","2015-09-29T00:00:00","2015-09-30T00:00:00","2015-10-01T00:00:00","2015-10-02T00:00:00","2015-10-05T00:00:00","2015-10-06T00:00:00","2015-10-07T00:00:00","2015-10-08T00:00:00","2015-10-09T00:00:00","2015-10-12T00:00:00","2015-10-13T00:00:00","2015-10-14T00:00:00","2015-10-15T00:00:00","2015-10-16T00:00:00","2015-10-19T00:00:00","2015-10-20T00:00:00","2015-10-21T00:00:00","2015-10-22T00:00:00","2015-10-23T00:00:00","2015-10-26T00:00:00","2015-10-27T00:00:00","2015-10-28T00:00:00","2015-10-29T00:00:00","2015-10-30T00:00:00","2015-11-02T00:00:00","2015-11-03T00:00:00","2015-11-04T00:00:00","2015-11-05T00:00:00","2015-11-06T00:00:00","2015-11-09T00:00:00","2015-11-10T00:00:00","2015-11-11T00:00:00","2015-11-12T00:00:00","2015-11-13T00:00:00","2015-11-16T00:00:00","2015-11-17T00:00:00","2015-11-18T00:00:00","2015-11-19T00:00:00","2015-11-20T00:00:00","2015-11-23T00:00:00","2015-11-24T00:00:00","2015-11-25T00:00:00","2015-11-27T00:00:00","2015-11-30T00:00:00","2015-12-01T00:00:00","2015-12-02T00:00:00","2015-12-03T00:00:00","2015-12-04T00:00:00","2015-12-07T00:00:00","2015-12-08T00:00:00","2015-12-09T00:00:00","2015-12-10T00:00:00","2015-12-11T00:00:00","2015-12-14T00:00:00","2015-12-15T00:00:00","2015-12-16T00:00:00","2015-12-17T00:00:00","2015-12-18T00:00:00","2015-12-21T00:00:00","2015-12-22T00:00:00","2015-12-23T00:00:00","2015-12-24T00:00:00","2015-12-28T00:00:00","2015-12-29T00:00:00","2015-12-30T00:00:00","2015-12-31T00:00:00","2016-01-04T00:00:00","2016-01-05T00:00:00","2016-01-06T00:00:00","2016-01-07T00:00:00","2016-01-08T00:00:00","2016-01-11T00:00:00","2016-01-12T00:00:00","2016-01-13T00:00:00","2016-01-14T00:00:00","2016-01-15T00:00:00","2016-01-19T00:00:00","2016-01-20T00:00:00","2016-01-21T00:00:00","2016-01-22T00:00:00","2016-01-25T00:00:00","2016-01-26T00:00:00","2016-01-27T00:00:00","2016-01-28T00:00:00","2016-01-29T00:00:00","2016-02-01T00:00:00","2016-02-02T00:00:00","2016-02-03T00:00:00","2016-02-04T00:00:00","2016-02-05T00:00:00","2016-02-08T00:00:00","2016-02-09T00:00:00","2016-02-10T00:00:00","2016-02-11T00:00:00","2016-02-12T00:00:00","2016-02-16T00:00:00","2016-02-17T00:00:00","2016-02-18T00:00:00","2016-02-19T00:00:00","2016-02-22T00:00:00","2016-02-23T00:00:00","2016-02-24T00:00:00","2016-02-25T00:00:00","2016-02-26T00:00:00","2016-02-29T00:00:00","2016-03-01T00:00:00","2016-03-02T00:00:00","2016-03-03T00:00:00","2016-03-04T00:00:00","2016-03-07T00:00:00","2016-03-08T00:00:00","2016-03-09T00:00:00","2016-03-10T00:00:00","2016-03-11T00:00:00","2016-03-14T00:00:00","2016-03-15T00:00:00","2016-03-16T00:00:00","2016-03-17T00:00:00","2016-03-18T00:00:00","2016-03-21T00:00:00","2016-03-22T00:00:00","2016-03-23T00:00:00","2016-03-24T00:00:00","2016-03-28T00:00:00","2016-03-29T00:00:00","2016-03-30T00:00:00","2016-03-31T00:00:00","2016-04-01T00:00:00","2016-04-04T00:00:00","2016-04-05T00:00:00","2016-04-06T00:00:00","2016-04-07T00:00:00","2016-04-08T00:00:00","2016-04-11T00:00:00","2016-04-12T00:00:00","2016-04-13T00:00:00","2016-04-14T00:00:00","2016-04-15T00:00:00","2016-04-18T00:00:00","2016-04-19T00:00:00","2016-04-20T00:00:00","2016-04-21T00:00:00","2016-04-22T00:00:00","2016-04-25T00:00:00","2016-04-26T00:00:00","2016-04-27T00:00:00","2016-04-28T00:00:00","2016-04-29T00:00:00","2016-05-02T00:00:00","2016-05-03T00:00:00","2016-05-04T00:00:00","2016-05-05T00:00:00","2016-05-06T00:00:00","2016-05-09T00:00:00","2016-05-10T00:00:00","2016-05-11T00:00:00","2016-05-12T00:00:00","2016-05-13T00:00:00","2016-05-16T00:00:00","2016-05-17T00:00:00","2016-05-18T00:00:00","2016-05-19T00:00:00","2016-05-20T00:00:00","2016-05-23T00:00:00","2016-05-24T00:00:00","2016-05-25T00:00:00","2016-05-26T00:00:00","2016-05-27T00:00:00","2016-05-31T00:00:00","2016-06-01T00:00:00","2016-06-02T00:00:00","2016-06-03T00:00:00","2016-06-06T00:00:00","2016-06-07T00:00:00","2016-06-08T00:00:00","2016-06-09T00:00:00","2016-06-10T00:00:00","2016-06-13T00:00:00","2016-06-14T00:00:00","2016-06-15T00:00:00","2016-06-16T00:00:00","2016-06-17T00:00:00","2016-06-20T00:00:00","2016-06-21T00:00:00","2016-06-22T00:00:00","2016-06-23T00:00:00","2016-06-24T00:00:00","2016-06-27T00:00:00","2016-06-28T00:00:00","2016-06-29T00:00:00","2016-06-30T00:00:00","2016-07-01T00:00:00","2016-07-05T00:00:00","2016-07-06T00:00:00","2016-07-07T00:00:00","2016-07-08T00:00:00","2016-07-11T00:00:00","2016-07-12T00:00:00","2016-07-13T00:00:00","2016-07-14T00:00:00","2016-07-15T00:00:00","2016-07-18T00:00:00","2016-07-19T00:00:00","2016-07-20T00:00:00","2016-07-21T00:00:00","2016-07-22T00:00:00","2016-07-25T00:00:00","2016-07-26T00:00:00","2016-07-27T00:00:00","2016-07-28T00:00:00","2016-07-29T00:00:00","2016-08-01T00:00:00","2016-08-02T00:00:00","2016-08-03T00:00:00","2016-08-04T00:00:00","2016-08-05T00:00:00","2016-08-08T00:00:00","2016-08-09T00:00:00","2016-08-10T00:00:00","2016-08-11T00:00:00","2016-08-12T00:00:00","2016-08-15T00:00:00","2016-08-16T00:00:00","2016-08-17T00:00:00","2016-08-18T00:00:00","2016-08-19T00:00:00","2016-08-22T00:00:00","2016-08-23T00:00:00","2016-08-24T00:00:00","2016-08-25T00:00:00","2016-08-26T00:00:00","2016-08-29T00:00:00","2016-08-30T00:00:00","2016-08-31T00:00:00","2016-09-01T00:00:00","2016-09-02T00:00:00","2016-09-06T00:00:00","2016-09-07T00:00:00","2016-09-08T00:00:00","2016-09-09T00:00:00","2016-09-12T00:00:00","2016-09-13T00:00:00","2016-09-14T00:00:00","2016-09-15T00:00:00","2016-09-16T00:00:00","2016-09-19T00:00:00","2016-09-20T00:00:00","2016-09-21T00:00:00","2016-09-22T00:00:00","2016-09-23T00:00:00","2016-09-26T00:00:00","2016-09-27T00:00:00","2016-09-28T00:00:00","2016-09-29T00:00:00","2016-09-30T00:00:00","2016-10-03T00:00:00","2016-10-04T00:00:00","2016-10-05T00:00:00","2016-10-06T00:00:00","2016-10-07T00:00:00","2016-10-10T00:00:00","2016-10-11T00:00:00","2016-10-12T00:00:00","2016-10-13T00:00:00","2016-10-14T00:00:00","2016-10-17T00:00:00","2016-10-18T00:00:00","2016-10-19T00:00:00","2016-10-20T00:00:00","2016-10-21T00:00:00","2016-10-24T00:00:00","2016-10-25T00:00:00","2016-10-26T00:00:00","2016-10-27T00:00:00","2016-10-28T00:00:00","2016-10-31T00:00:00","2016-11-01T00:00:00","2016-11-02T00:00:00","2016-11-03T00:00:00","2016-11-04T00:00:00","2016-11-07T00:00:00","2016-11-08T00:00:00","2016-11-09T00:00:00","2016-11-10T00:00:00","2016-11-11T00:00:00","2016-11-14T00:00:00","2016-11-15T00:00:00","2016-11-16T00:00:00","2016-11-17T00:00:00","2016-11-18T00:00:00","2016-11-21T00:00:00","2016-11-22T00:00:00","2016-11-23T00:00:00","2016-11-25T00:00:00","2016-11-28T00:00:00","2016-11-29T00:00:00","2016-11-30T00:00:00","2016-12-01T00:00:00","2016-12-02T00:00:00","2016-12-05T00:00:00","2016-12-06T00:00:00","2016-12-07T00:00:00","2016-12-08T00:00:00","2016-12-09T00:00:00","2016-12-12T00:00:00","2016-12-13T00:00:00","2016-12-14T00:00:00","2016-12-15T00:00:00","2016-12-16T00:00:00","2016-12-19T00:00:00","2016-12-20T00:00:00","2016-12-21T00:00:00","2016-12-22T00:00:00","2016-12-23T00:00:00","2016-12-27T00:00:00","2016-12-28T00:00:00","2016-12-29T00:00:00","2016-12-30T00:00:00","2017-01-03T00:00:00","2017-01-04T00:00:00","2017-01-05T00:00:00","2017-01-06T00:00:00","2017-01-09T00:00:00","2017-01-10T00:00:00","2017-01-11T00:00:00","2017-01-12T00:00:00","2017-01-13T00:00:00","2017-01-17T00:00:00","2017-01-18T00:00:00","2017-01-19T00:00:00","2017-01-20T00:00:00","2017-01-23T00:00:00","2017-01-24T00:00:00","2017-01-25T00:00:00","2017-01-26T00:00:00","2017-01-27T00:00:00","2017-01-30T00:00:00","2017-01-31T00:00:00","2017-02-01T00:00:00","2017-02-02T00:00:00","2017-02-03T00:00:00","2017-02-06T00:00:00","2017-02-07T00:00:00","2017-02-08T00:00:00","2017-02-09T00:00:00","2017-02-10T00:00:00","2017-02-13T00:00:00","2017-02-14T00:00:00","2017-02-15T00:00:00","2017-02-16T00:00:00","2017-02-17T00:00:00","2017-02-21T00:00:00","2017-02-22T00:00:00","2017-02-23T00:00:00","2017-02-24T00:00:00","2017-02-27T00:00:00","2017-02-28T00:00:00","2017-03-01T00:00:00","2017-03-02T00:00:00","2017-03-03T00:00:00","2017-03-06T00:00:00","2017-03-07T00:00:00","2017-03-08T00:00:00","2017-03-09T00:00:00","2017-03-10T00:00:00","2017-03-13T00:00:00","2017-03-14T00:00:00","2017-03-15T00:00:00","2017-03-16T00:00:00","2017-03-17T00:00:00","2017-03-20T00:00:00","2017-03-21T00:00:00","2017-03-22T00:00:00","2017-03-23T00:00:00","2017-03-24T00:00:00","2017-03-27T00:00:00","2017-03-28T00:00:00","2017-03-29T00:00:00","2017-03-30T00:00:00","2017-03-31T00:00:00","2017-04-03T00:00:00","2017-04-04T00:00:00","2017-04-05T00:00:00","2017-04-06T00:00:00","2017-04-07T00:00:00","2017-04-10T00:00:00","2017-04-11T00:00:00","2017-04-12T00:00:00","2017-04-13T00:00:00","2017-04-17T00:00:00","2017-04-18T00:00:00","2017-04-19T00:00:00","2017-04-20T00:00:00","2017-04-21T00:00:00","2017-04-24T00:00:00","2017-04-25T00:00:00","2017-04-26T00:00:00","2017-04-27T00:00:00","2017-04-28T00:00:00","2017-05-01T00:00:00","2017-05-02T00:00:00","2017-05-03T00:00:00","2017-05-04T00:00:00","2017-05-05T00:00:00","2017-05-08T00:00:00","2017-05-09T00:00:00","2017-05-10T00:00:00","2017-05-11T00:00:00","2017-05-12T00:00:00","2017-05-15T00:00:00","2017-05-16T00:00:00","2017-05-17T00:00:00","2017-05-18T00:00:00","2017-05-19T00:00:00","2017-05-22T00:00:00","2017-05-23T00:00:00","2017-05-24T00:00:00","2017-05-25T00:00:00","2017-05-26T00:00:00","2017-05-30T00:00:00","2017-05-31T00:00:00","2017-06-01T00:00:00","2017-06-02T00:00:00","2017-06-05T00:00:00","2017-06-06T00:00:00","2017-06-07T00:00:00","2017-06-08T00:00:00","2017-06-09T00:00:00","2017-06-12T00:00:00","2017-06-13T00:00:00","2017-06-14T00:00:00","2017-06-15T00:00:00","2017-06-16T00:00:00","2017-06-19T00:00:00","2017-06-20T00:00:00","2017-06-21T00:00:00","2017-06-22T00:00:00","2017-06-23T00:00:00","2017-06-26T00:00:00","2017-06-27T00:00:00","2017-06-28T00:00:00","2017-06-29T00:00:00","2017-06-30T00:00:00","2017-07-03T00:00:00","2017-07-05T00:00:00","2017-07-06T00:00:00","2017-07-07T00:00:00","2017-07-10T00:00:00","2017-07-11T00:00:00","2017-07-12T00:00:00","2017-07-13T00:00:00","2017-07-14T00:00:00","2017-07-17T00:00:00","2017-07-18T00:00:00","2017-07-19T00:00:00","2017-07-20T00:00:00","2017-07-21T00:00:00","2017-07-24T00:00:00","2017-07-25T00:00:00","2017-07-26T00:00:00","2017-07-27T00:00:00","2017-07-28T00:00:00","2017-07-31T00:00:00","2017-08-01T00:00:00","2017-08-02T00:00:00","2017-08-03T00:00:00","2017-08-04T00:00:00","2017-08-07T00:00:00","2017-08-08T00:00:00","2017-08-09T00:00:00","2017-08-10T00:00:00","2017-08-11T00:00:00","2017-08-14T00:00:00","2017-08-15T00:00:00","2017-08-16T00:00:00","2017-08-17T00:00:00","2017-08-18T00:00:00","2017-08-21T00:00:00","2017-08-22T00:00:00","2017-08-23T00:00:00","2017-08-24T00:00:00","2017-08-25T00:00:00","2017-08-28T00:00:00","2017-08-29T00:00:00","2017-08-30T00:00:00","2017-08-31T00:00:00","2017-09-01T00:00:00","2017-09-05T00:00:00","2017-09-06T00:00:00","2017-09-07T00:00:00","2017-09-08T00:00:00","2017-09-11T00:00:00","2017-09-12T00:00:00","2017-09-13T00:00:00","2017-09-14T00:00:00","2017-09-15T00:00:00","2017-09-18T00:00:00","2017-09-19T00:00:00","2017-09-20T00:00:00","2017-09-21T00:00:00","2017-09-22T00:00:00","2017-09-25T00:00:00","2017-09-26T00:00:00","2017-09-27T00:00:00","2017-09-28T00:00:00","2017-09-29T00:00:00","2017-10-02T00:00:00","2017-10-03T00:00:00","2017-10-04T00:00:00","2017-10-05T00:00:00","2017-10-06T00:00:00","2017-10-09T00:00:00","2017-10-10T00:00:00","2017-10-11T00:00:00","2017-10-12T00:00:00","2017-10-13T00:00:00","2017-10-16T00:00:00","2017-10-17T00:00:00","2017-10-18T00:00:00","2017-10-19T00:00:00","2017-10-20T00:00:00","2017-10-23T00:00:00","2017-10-24T00:00:00","2017-10-25T00:00:00","2017-10-26T00:00:00","2017-10-27T00:00:00","2017-10-30T00:00:00","2017-10-31T00:00:00","2017-11-01T00:00:00","2017-11-02T00:00:00","2017-11-03T00:00:00","2017-11-06T00:00:00","2017-11-07T00:00:00","2017-11-08T00:00:00","2017-11-09T00:00:00","2017-11-10T00:00:00","2017-11-13T00:00:00","2017-11-14T00:00:00","2017-11-15T00:00:00","2017-11-16T00:00:00","2017-11-17T00:00:00","2017-11-20T00:00:00","2017-11-21T00:00:00","2017-11-22T00:00:00","2017-11-24T00:00:00","2017-11-27T00:00:00","2017-11-28T00:00:00","2017-11-29T00:00:00","2017-11-30T00:00:00","2017-12-01T00:00:00","2017-12-04T00:00:00","2017-12-05T00:00:00","2017-12-06T00:00:00","2017-12-07T00:00:00","2017-12-08T00:00:00","2017-12-11T00:00:00","2017-12-12T00:00:00","2017-12-13T00:00:00","2017-12-14T00:00:00","2017-12-15T00:00:00","2017-12-18T00:00:00","2017-12-19T00:00:00","2017-12-20T00:00:00","2017-12-21T00:00:00","2017-12-22T00:00:00","2017-12-26T00:00:00","2017-12-27T00:00:00","2017-12-28T00:00:00","2017-12-29T00:00:00","2018-01-02T00:00:00","2018-01-03T00:00:00","2018-01-04T00:00:00","2018-01-05T00:00:00","2018-01-08T00:00:00","2018-01-09T00:00:00","2018-01-10T00:00:00","2018-01-11T00:00:00","2018-01-12T00:00:00","2018-01-16T00:00:00","2018-01-17T00:00:00","2018-01-18T00:00:00","2018-01-19T00:00:00","2018-01-22T00:00:00","2018-01-23T00:00:00","2018-01-24T00:00:00","2018-01-25T00:00:00","2018-01-26T00:00:00","2018-01-29T00:00:00","2018-01-30T00:00:00","2018-01-31T00:00:00","2018-02-01T00:00:00","2018-02-02T00:00:00","2018-02-05T00:00:00","2018-02-06T00:00:00","2018-02-07T00:00:00","2018-02-08T00:00:00","2018-02-09T00:00:00","2018-02-12T00:00:00","2018-02-13T00:00:00","2018-02-14T00:00:00","2018-02-15T00:00:00","2018-02-16T00:00:00","2018-02-20T00:00:00","2018-02-21T00:00:00","2018-02-22T00:00:00","2018-02-23T00:00:00","2018-02-26T00:00:00","2018-02-27T00:00:00","2018-02-28T00:00:00","2018-03-01T00:00:00","2018-03-02T00:00:00","2018-03-05T00:00:00","2018-03-06T00:00:00","2018-03-07T00:00:00","2018-03-08T00:00:00","2018-03-09T00:00:00","2018-03-12T00:00:00","2018-03-13T00:00:00","2018-03-14T00:00:00","2018-03-15T00:00:00","2018-03-16T00:00:00","2018-03-19T00:00:00","2018-03-20T00:00:00","2018-03-21T00:00:00","2018-03-22T00:00:00","2018-03-23T00:00:00","2018-03-26T00:00:00","2018-03-27T00:00:00","2018-03-28T00:00:00","2018-03-29T00:00:00","2018-04-02T00:00:00","2018-04-03T00:00:00","2018-04-04T00:00:00","2018-04-05T00:00:00","2018-04-06T00:00:00","2018-04-09T00:00:00","2018-04-10T00:00:00","2018-04-11T00:00:00","2018-04-12T00:00:00","2018-04-13T00:00:00","2018-04-16T00:00:00","2018-04-17T00:00:00","2018-04-18T00:00:00","2018-04-19T00:00:00","2018-04-20T00:00:00","2018-04-23T00:00:00","2018-04-24T00:00:00","2018-04-25T00:00:00","2018-04-26T00:00:00","2018-04-27T00:00:00","2018-04-30T00:00:00","2018-05-01T00:00:00","2018-05-02T00:00:00","2018-05-03T00:00:00","2018-05-04T00:00:00","2018-05-07T00:00:00","2018-05-08T00:00:00","2018-05-09T00:00:00","2018-05-10T00:00:00","2018-05-11T00:00:00","2018-05-14T00:00:00","2018-05-15T00:00:00","2018-05-16T00:00:00","2018-05-17T00:00:00","2018-05-18T00:00:00","2018-05-21T00:00:00","2018-05-22T00:00:00","2018-05-23T00:00:00","2018-05-24T00:00:00","2018-05-25T00:00:00","2018-05-29T00:00:00","2018-05-30T00:00:00","2018-05-31T00:00:00","2018-06-01T00:00:00","2018-06-04T00:00:00","2018-06-05T00:00:00","2018-06-06T00:00:00","2018-06-07T00:00:00","2018-06-08T00:00:00","2018-06-11T00:00:00","2018-06-12T00:00:00","2018-06-13T00:00:00","2018-06-14T00:00:00","2018-06-15T00:00:00","2018-06-18T00:00:00","2018-06-19T00:00:00","2018-06-20T00:00:00","2018-06-21T00:00:00","2018-06-22T00:00:00","2018-06-25T00:00:00","2018-06-26T00:00:00","2018-06-27T00:00:00","2018-06-28T00:00:00","2018-06-29T00:00:00","2018-07-02T00:00:00","2018-07-03T00:00:00","2018-07-05T00:00:00","2018-07-06T00:00:00","2018-07-09T00:00:00","2018-07-10T00:00:00","2018-07-11T00:00:00","2018-07-12T00:00:00","2018-07-13T00:00:00","2018-07-16T00:00:00","2018-07-17T00:00:00","2018-07-18T00:00:00","2018-07-19T00:00:00","2018-07-20T00:00:00","2018-07-23T00:00:00","2018-07-24T00:00:00","2018-07-25T00:00:00","2018-07-26T00:00:00","2018-07-27T00:00:00","2018-07-30T00:00:00","2018-07-31T00:00:00","2018-08-01T00:00:00","2018-08-02T00:00:00","2018-08-03T00:00:00","2018-08-06T00:00:00","2018-08-07T00:00:00","2018-08-08T00:00:00","2018-08-09T00:00:00","2018-08-10T00:00:00","2018-08-13T00:00:00","2018-08-14T00:00:00","2018-08-15T00:00:00","2018-08-16T00:00:00","2018-08-17T00:00:00","2018-08-20T00:00:00","2018-08-21T00:00:00","2018-08-22T00:00:00","2018-08-23T00:00:00","2018-08-24T00:00:00","2018-08-27T00:00:00","2018-08-28T00:00:00","2018-08-29T00:00:00","2018-08-30T00:00:00","2018-08-31T00:00:00","2018-09-04T00:00:00","2018-09-05T00:00:00","2018-09-06T00:00:00","2018-09-07T00:00:00","2018-09-10T00:00:00","2018-09-11T00:00:00","2018-09-12T00:00:00","2018-09-13T00:00:00","2018-09-14T00:00:00","2018-09-17T00:00:00","2018-09-18T00:00:00","2018-09-19T00:00:00","2018-09-20T00:00:00","2018-09-21T00:00:00","2018-09-24T00:00:00","2018-09-25T00:00:00","2018-09-26T00:00:00","2018-09-27T00:00:00","2018-09-28T00:00:00","2018-10-01T00:00:00","2018-10-02T00:00:00","2018-10-03T00:00:00","2018-10-04T00:00:00","2018-10-05T00:00:00","2018-10-08T00:00:00","2018-10-09T00:00:00","2018-10-10T00:00:00","2018-10-11T00:00:00","2018-10-12T00:00:00","2018-10-15T00:00:00","2018-10-16T00:00:00","2018-10-17T00:00:00","2018-10-18T00:00:00","2018-10-19T00:00:00","2018-10-22T00:00:00","2018-10-23T00:00:00","2018-10-24T00:00:00","2018-10-25T00:00:00","2018-10-26T00:00:00","2018-10-29T00:00:00","2018-10-30T00:00:00","2018-10-31T00:00:00","2018-11-01T00:00:00","2018-11-02T00:00:00","2018-11-05T00:00:00","2018-11-06T00:00:00","2018-11-07T00:00:00","2018-11-08T00:00:00","2018-11-09T00:00:00","2018-11-12T00:00:00","2018-11-13T00:00:00","2018-11-14T00:00:00","2018-11-15T00:00:00","2018-11-16T00:00:00","2018-11-19T00:00:00","2018-11-20T00:00:00","2018-11-21T00:00:00","2018-11-23T00:00:00","2018-11-26T00:00:00","2018-11-27T00:00:00","2018-11-28T00:00:00","2018-11-29T00:00:00","2018-11-30T00:00:00","2018-12-03T00:00:00","2018-12-04T00:00:00","2018-12-06T00:00:00","2018-12-07T00:00:00","2018-12-10T00:00:00","2018-12-11T00:00:00","2018-12-12T00:00:00","2018-12-13T00:00:00","2018-12-14T00:00:00","2018-12-17T00:00:00","2018-12-18T00:00:00","2018-12-19T00:00:00","2018-12-20T00:00:00","2018-12-21T00:00:00","2018-12-24T00:00:00","2018-12-26T00:00:00","2018-12-27T00:00:00","2018-12-28T00:00:00","2018-12-31T00:00:00","2019-01-02T00:00:00","2019-01-03T00:00:00","2019-01-04T00:00:00","2019-01-07T00:00:00","2019-01-08T00:00:00","2019-01-09T00:00:00","2019-01-10T00:00:00","2019-01-11T00:00:00","2019-01-14T00:00:00","2019-01-15T00:00:00","2019-01-16T00:00:00","2019-01-17T00:00:00","2019-01-18T00:00:00","2019-01-22T00:00:00","2019-01-23T00:00:00","2019-01-24T00:00:00","2019-01-25T00:00:00","2019-01-28T00:00:00","2019-01-29T00:00:00","2019-01-30T00:00:00","2019-01-31T00:00:00","2019-02-01T00:00:00","2019-02-04T00:00:00","2019-02-05T00:00:00","2019-02-06T00:00:00","2019-02-07T00:00:00","2019-02-08T00:00:00","2019-02-11T00:00:00","2019-02-12T00:00:00","2019-02-13T00:00:00","2019-02-14T00:00:00","2019-02-15T00:00:00","2019-02-19T00:00:00","2019-02-20T00:00:00","2019-02-21T00:00:00","2019-02-22T00:00:00","2019-02-25T00:00:00","2019-02-26T00:00:00","2019-02-27T00:00:00","2019-02-28T00:00:00","2019-03-01T00:00:00","2019-03-04T00:00:00","2019-03-05T00:00:00","2019-03-06T00:00:00","2019-03-07T00:00:00","2019-03-08T00:00:00","2019-03-11T00:00:00","2019-03-12T00:00:00","2019-03-13T00:00:00","2019-03-14T00:00:00","2019-03-15T00:00:00","2019-03-18T00:00:00","2019-03-19T00:00:00","2019-03-20T00:00:00","2019-03-21T00:00:00","2019-03-22T00:00:00","2019-03-25T00:00:00","2019-03-26T00:00:00","2019-03-27T00:00:00","2019-03-28T00:00:00","2019-03-29T00:00:00","2019-04-01T00:00:00","2019-04-02T00:00:00","2019-04-03T00:00:00","2019-04-04T00:00:00","2019-04-05T00:00:00","2019-04-08T00:00:00","2019-04-09T00:00:00","2019-04-10T00:00:00","2019-04-11T00:00:00","2019-04-12T00:00:00","2019-04-15T00:00:00","2019-04-16T00:00:00","2019-04-17T00:00:00","2019-04-18T00:00:00","2019-04-22T00:00:00","2019-04-23T00:00:00","2019-04-24T00:00:00","2019-04-25T00:00:00","2019-04-26T00:00:00","2019-04-29T00:00:00","2019-04-30T00:00:00","2019-05-01T00:00:00","2019-05-02T00:00:00","2019-05-03T00:00:00","2019-05-06T00:00:00","2019-05-07T00:00:00","2019-05-08T00:00:00","2019-05-09T00:00:00","2019-05-10T00:00:00","2019-05-13T00:00:00","2019-05-14T00:00:00","2019-05-15T00:00:00","2019-05-16T00:00:00","2019-05-17T00:00:00","2019-05-20T00:00:00","2019-05-21T00:00:00","2019-05-22T00:00:00","2019-05-23T00:00:00","2019-05-24T00:00:00","2019-05-28T00:00:00","2019-05-29T00:00:00","2019-05-30T00:00:00","2019-05-31T00:00:00","2019-06-03T00:00:00","2019-06-04T00:00:00","2019-06-05T00:00:00","2019-06-06T00:00:00","2019-06-07T00:00:00","2019-06-10T00:00:00","2019-06-11T00:00:00","2019-06-12T00:00:00","2019-06-13T00:00:00","2019-06-14T00:00:00","2019-06-17T00:00:00","2019-06-18T00:00:00","2019-06-19T00:00:00","2019-06-20T00:00:00","2019-06-21T00:00:00","2019-06-24T00:00:00","2019-06-25T00:00:00","2019-06-26T00:00:00","2019-06-27T00:00:00","2019-06-28T00:00:00","2019-07-01T00:00:00","2019-07-02T00:00:00","2019-07-03T00:00:00","2019-07-05T00:00:00","2019-07-08T00:00:00","2019-07-09T00:00:00","2019-07-10T00:00:00","2019-07-11T00:00:00","2019-07-12T00:00:00","2019-07-15T00:00:00","2019-07-16T00:00:00","2019-07-17T00:00:00","2019-07-18T00:00:00","2019-07-19T00:00:00","2019-07-22T00:00:00","2019-07-23T00:00:00","2019-07-24T00:00:00","2019-07-25T00:00:00","2019-07-26T00:00:00","2019-07-29T00:00:00","2019-07-30T00:00:00","2019-07-31T00:00:00","2019-08-01T00:00:00","2019-08-02T00:00:00","2019-08-05T00:00:00","2019-08-06T00:00:00","2019-08-07T00:00:00","2019-08-08T00:00:00","2019-08-09T00:00:00","2019-08-12T00:00:00","2019-08-13T00:00:00","2019-08-14T00:00:00","2019-08-15T00:00:00","2019-08-16T00:00:00","2019-08-19T00:00:00","2019-08-20T00:00:00","2019-08-21T00:00:00","2019-08-22T00:00:00","2019-08-23T00:00:00","2019-08-26T00:00:00","2019-08-27T00:00:00","2019-08-28T00:00:00","2019-08-29T00:00:00","2019-08-30T00:00:00","2019-09-03T00:00:00","2019-09-04T00:00:00","2019-09-05T00:00:00","2019-09-06T00:00:00","2019-09-09T00:00:00","2019-09-10T00:00:00","2019-09-11T00:00:00","2019-09-12T00:00:00","2019-09-13T00:00:00","2019-09-16T00:00:00","2019-09-17T00:00:00","2019-09-18T00:00:00","2019-09-19T00:00:00","2019-09-20T00:00:00","2019-09-23T00:00:00","2019-09-24T00:00:00","2019-09-25T00:00:00","2019-09-26T00:00:00","2019-09-27T00:00:00","2019-09-30T00:00:00","2019-10-01T00:00:00","2019-10-02T00:00:00","2019-10-03T00:00:00","2019-10-04T00:00:00","2019-10-07T00:00:00","2019-10-08T00:00:00","2019-10-09T00:00:00","2019-10-10T00:00:00","2019-10-11T00:00:00","2019-10-14T00:00:00","2019-10-15T00:00:00","2019-10-16T00:00:00","2019-10-17T00:00:00","2019-10-18T00:00:00","2019-10-21T00:00:00","2019-10-22T00:00:00","2019-10-23T00:00:00","2019-10-24T00:00:00","2019-10-25T00:00:00","2019-10-28T00:00:00","2019-10-29T00:00:00","2019-10-30T00:00:00","2019-10-31T00:00:00","2019-11-01T00:00:00","2019-11-04T00:00:00","2019-11-05T00:00:00","2019-11-06T00:00:00","2019-11-07T00:00:00","2019-11-08T00:00:00","2019-11-11T00:00:00","2019-11-12T00:00:00","2019-11-13T00:00:00","2019-11-14T00:00:00","2019-11-15T00:00:00","2019-11-18T00:00:00","2019-11-19T00:00:00","2019-11-20T00:00:00","2019-11-21T00:00:00","2019-11-22T00:00:00","2019-11-25T00:00:00","2019-11-26T00:00:00","2019-11-27T00:00:00","2019-11-29T00:00:00","2019-12-02T00:00:00","2019-12-03T00:00:00","2019-12-04T00:00:00","2019-12-05T00:00:00","2019-12-06T00:00:00","2019-12-09T00:00:00","2019-12-10T00:00:00","2019-12-11T00:00:00","2019-12-12T00:00:00","2019-12-13T00:00:00","2019-12-16T00:00:00","2019-12-17T00:00:00","2019-12-18T00:00:00","2019-12-19T00:00:00","2019-12-20T00:00:00","2019-12-23T00:00:00","2019-12-24T00:00:00","2019-12-26T00:00:00","2019-12-27T00:00:00","2019-12-30T00:00:00","2019-12-31T00:00:00","2020-01-02T00:00:00","2020-01-03T00:00:00","2020-01-06T00:00:00","2020-01-07T00:00:00","2020-01-08T00:00:00","2020-01-09T00:00:00","2020-01-10T00:00:00","2020-01-13T00:00:00","2020-01-14T00:00:00","2020-01-15T00:00:00","2020-01-16T00:00:00","2020-01-17T00:00:00","2020-01-21T00:00:00","2020-01-22T00:00:00","2020-01-23T00:00:00","2020-01-24T00:00:00","2020-01-27T00:00:00","2020-01-28T00:00:00","2020-01-29T00:00:00","2020-01-30T00:00:00","2020-01-31T00:00:00","2020-02-03T00:00:00","2020-02-04T00:00:00","2020-02-05T00:00:00","2020-02-06T00:00:00","2020-02-07T00:00:00","2020-02-10T00:00:00","2020-02-11T00:00:00","2020-02-12T00:00:00","2020-02-13T00:00:00","2020-02-14T00:00:00","2020-02-18T00:00:00","2020-02-19T00:00:00","2020-02-20T00:00:00","2020-02-21T00:00:00","2020-02-24T00:00:00","2020-02-25T00:00:00","2020-02-26T00:00:00","2020-02-27T00:00:00","2020-02-28T00:00:00","2020-03-02T00:00:00","2020-03-03T00:00:00","2020-03-04T00:00:00","2020-03-05T00:00:00","2020-03-06T00:00:00","2020-03-09T00:00:00","2020-03-10T00:00:00","2020-03-11T00:00:00","2020-03-12T00:00:00","2020-03-13T00:00:00","2020-03-16T00:00:00","2020-03-17T00:00:00","2020-03-18T00:00:00","2020-03-19T00:00:00","2020-03-20T00:00:00","2020-03-23T00:00:00","2020-03-24T00:00:00","2020-03-25T00:00:00","2020-03-26T00:00:00","2020-03-27T00:00:00","2020-03-30T00:00:00","2020-03-31T00:00:00","2020-04-01T00:00:00","2020-04-02T00:00:00","2020-04-03T00:00:00","2020-04-06T00:00:00","2020-04-07T00:00:00","2020-04-08T00:00:00","2020-04-09T00:00:00","2020-04-13T00:00:00","2020-04-14T00:00:00","2020-04-15T00:00:00","2020-04-16T00:00:00","2020-04-17T00:00:00","2020-04-20T00:00:00","2020-04-21T00:00:00","2020-04-22T00:00:00","2020-04-23T00:00:00","2020-04-24T00:00:00","2020-04-27T00:00:00","2020-04-28T00:00:00","2020-04-29T00:00:00","2020-04-30T00:00:00","2020-05-01T00:00:00","2020-05-04T00:00:00","2020-05-05T00:00:00","2020-05-06T00:00:00","2020-05-07T00:00:00","2020-05-08T00:00:00","2020-05-11T00:00:00","2020-05-12T00:00:00","2020-05-13T00:00:00","2020-05-14T00:00:00","2020-05-15T00:00:00","2020-05-18T00:00:00","2020-05-19T00:00:00","2020-05-20T00:00:00","2020-05-21T00:00:00","2020-05-22T00:00:00","2020-05-26T00:00:00","2020-05-27T00:00:00","2020-05-28T00:00:00","2020-05-29T00:00:00","2020-06-01T00:00:00","2020-06-02T00:00:00","2020-06-03T00:00:00","2020-06-04T00:00:00","2020-06-05T00:00:00","2020-06-08T00:00:00","2020-06-09T00:00:00","2020-06-10T00:00:00","2020-06-11T00:00:00","2020-06-12T00:00:00","2020-06-15T00:00:00","2020-06-16T00:00:00","2020-06-17T00:00:00","2020-06-18T00:00:00","2020-06-19T00:00:00","2020-06-22T00:00:00","2020-06-23T00:00:00","2020-06-24T00:00:00","2020-06-25T00:00:00","2020-06-26T00:00:00","2020-06-29T00:00:00","2020-06-30T00:00:00","2020-07-01T00:00:00","2020-07-02T00:00:00","2020-07-06T00:00:00","2020-07-07T00:00:00","2020-07-08T00:00:00","2020-07-09T00:00:00","2020-07-10T00:00:00","2020-07-13T00:00:00","2020-07-14T00:00:00","2020-07-15T00:00:00","2020-07-16T00:00:00","2020-07-17T00:00:00","2020-07-20T00:00:00","2020-07-21T00:00:00","2020-07-22T00:00:00","2020-07-23T00:00:00","2020-07-24T00:00:00","2020-07-27T00:00:00","2020-07-28T00:00:00","2020-07-29T00:00:00","2020-07-30T00:00:00","2020-07-31T00:00:00","2020-08-03T00:00:00","2020-08-04T00:00:00","2020-08-05T00:00:00","2020-08-06T00:00:00","2020-08-07T00:00:00","2020-08-10T00:00:00","2020-08-11T00:00:00","2020-08-12T00:00:00","2020-08-13T00:00:00","2020-08-14T00:00:00","2020-08-17T00:00:00","2020-08-18T00:00:00","2020-08-19T00:00:00","2020-08-20T00:00:00","2020-08-21T00:00:00","2020-08-24T00:00:00","2020-08-25T00:00:00","2020-08-26T00:00:00","2020-08-27T00:00:00","2020-08-28T00:00:00","2020-08-31T00:00:00","2020-09-01T00:00:00","2020-09-02T00:00:00","2020-09-03T00:00:00","2020-09-04T00:00:00","2020-09-08T00:00:00","2020-09-09T00:00:00","2020-09-10T00:00:00","2020-09-11T00:00:00","2020-09-14T00:00:00","2020-09-15T00:00:00","2020-09-16T00:00:00","2020-09-17T00:00:00","2020-09-18T00:00:00","2020-09-21T00:00:00","2020-09-22T00:00:00","2020-09-23T00:00:00","2020-09-24T00:00:00","2020-09-25T00:00:00","2020-09-28T00:00:00","2020-09-29T00:00:00","2020-09-30T00:00:00","2020-10-01T00:00:00","2020-10-02T00:00:00","2020-10-05T00:00:00","2020-10-06T00:00:00","2020-10-07T00:00:00","2020-10-08T00:00:00","2020-10-09T00:00:00","2020-10-12T00:00:00","2020-10-13T00:00:00","2020-10-14T00:00:00","2020-10-15T00:00:00","2020-10-16T00:00:00","2020-10-19T00:00:00","2020-10-20T00:00:00","2020-10-21T00:00:00","2020-10-22T00:00:00","2020-10-23T00:00:00","2020-10-26T00:00:00","2020-10-27T00:00:00","2020-10-28T00:00:00","2020-10-29T00:00:00","2020-10-30T00:00:00","2020-11-02T00:00:00","2020-11-03T00:00:00","2020-11-04T00:00:00","2020-11-05T00:00:00","2020-11-06T00:00:00","2020-11-09T00:00:00","2020-11-10T00:00:00","2020-11-11T00:00:00","2020-11-12T00:00:00","2020-11-13T00:00:00","2020-11-16T00:00:00","2020-11-17T00:00:00","2020-11-18T00:00:00","2020-11-19T00:00:00","2020-11-20T00:00:00","2020-11-23T00:00:00","2020-11-24T00:00:00","2020-11-25T00:00:00","2020-11-27T00:00:00","2020-11-30T00:00:00","2020-12-01T00:00:00","2020-12-02T00:00:00","2020-12-03T00:00:00","2020-12-04T00:00:00","2020-12-07T00:00:00","2020-12-08T00:00:00","2020-12-09T00:00:00","2020-12-10T00:00:00","2020-12-11T00:00:00","2020-12-14T00:00:00","2020-12-15T00:00:00","2020-12-16T00:00:00","2020-12-17T00:00:00","2020-12-18T00:00:00","2020-12-21T00:00:00","2020-12-22T00:00:00","2020-12-23T00:00:00","2020-12-24T00:00:00","2020-12-28T00:00:00","2020-12-29T00:00:00","2020-12-30T00:00:00","2020-12-31T00:00:00","2021-01-04T00:00:00","2021-01-05T00:00:00","2021-01-06T00:00:00","2021-01-07T00:00:00","2021-01-08T00:00:00","2021-01-11T00:00:00","2021-01-12T00:00:00","2021-01-13T00:00:00","2021-01-14T00:00:00","2021-01-15T00:00:00","2021-01-19T00:00:00","2021-01-20T00:00:00","2021-01-21T00:00:00","2021-01-22T00:00:00","2021-01-25T00:00:00","2021-01-26T00:00:00","2021-01-27T00:00:00","2021-01-28T00:00:00","2021-01-29T00:00:00","2021-02-01T00:00:00","2021-02-02T00:00:00","2021-02-03T00:00:00","2021-02-04T00:00:00","2021-02-05T00:00:00","2021-02-08T00:00:00","2021-02-09T00:00:00","2021-02-10T00:00:00","2021-02-11T00:00:00","2021-02-12T00:00:00","2021-02-16T00:00:00","2021-02-17T00:00:00","2021-02-18T00:00:00","2021-02-19T00:00:00","2021-02-22T00:00:00","2021-02-23T00:00:00","2021-02-24T00:00:00","2021-02-25T00:00:00","2021-02-26T00:00:00","2021-03-01T00:00:00","2021-03-02T00:00:00","2021-03-03T00:00:00","2021-03-04T00:00:00","2021-03-05T00:00:00","2021-03-08T00:00:00","2021-03-09T00:00:00","2021-03-10T00:00:00","2021-03-11T00:00:00","2021-03-12T00:00:00","2021-03-15T00:00:00","2021-03-16T00:00:00","2021-03-17T00:00:00","2021-03-18T00:00:00","2021-03-19T00:00:00","2021-03-22T00:00:00","2021-03-23T00:00:00","2021-03-24T00:00:00","2021-03-25T00:00:00","2021-03-26T00:00:00","2021-03-29T00:00:00","2021-03-30T00:00:00","2021-03-31T00:00:00","2021-04-01T00:00:00","2021-04-05T00:00:00","2021-04-06T00:00:00","2021-04-07T00:00:00","2021-04-08T00:00:00","2021-04-09T00:00:00","2021-04-12T00:00:00","2021-04-13T00:00:00","2021-04-14T00:00:00","2021-04-15T00:00:00","2021-04-16T00:00:00","2021-04-19T00:00:00","2021-04-20T00:00:00","2021-04-21T00:00:00","2021-04-22T00:00:00","2021-04-23T00:00:00","2021-04-26T00:00:00","2021-04-27T00:00:00","2021-04-28T00:00:00","2021-04-29T00:00:00","2021-04-30T00:00:00","2021-05-03T00:00:00","2021-05-04T00:00:00","2021-05-05T00:00:00","2021-05-06T00:00:00","2021-05-07T00:00:00","2021-05-10T00:00:00","2021-05-11T00:00:00","2021-05-12T00:00:00","2021-05-13T00:00:00","2021-05-14T00:00:00","2021-05-17T00:00:00","2021-05-18T00:00:00","2021-05-19T00:00:00","2021-05-20T00:00:00","2021-05-21T00:00:00","2021-05-24T00:00:00","2021-05-25T00:00:00","2021-05-26T00:00:00","2021-05-27T00:00:00","2021-05-28T00:00:00","2021-06-01T00:00:00","2021-06-02T00:00:00","2021-06-03T00:00:00","2021-06-04T00:00:00","2021-06-07T00:00:00","2021-06-08T00:00:00","2021-06-09T00:00:00","2021-06-10T00:00:00","2021-06-11T00:00:00","2021-06-14T00:00:00"],"y":[1.6916664838790894,1.6832505464553833,1.6748337745666504,1.60750412940979,1.662209391593933,1.65800142288208,1.6285449266433716,1.6411689519882202,1.6411689519882202,1.611711859703064,1.60750412940979,1.6302279233932495,1.65800142288208,1.6201286315917969,1.6285449266433716,1.71859872341156,1.7589964866638184,1.7817208766937256,1.784245491027832,1.7690962553024292,1.767412781715393,1.71270751953125,1.6243363618850708,1.5738393068313599,1.5166085958480835,1.5780473947525024,1.6243363618850708,1.659684658050537,1.6815670728683472,1.733747959136963,1.7000824213027954,1.6032955646514893,1.568789005279541,1.5654231309890747,1.5948798656463623,1.5561648607254028,1.540174126625061,1.5948798656463623,1.5923551321029663,1.5570067167282104,1.535966157913208,1.5620564222335815,1.599088430404663,1.6672594547271729,1.6672594547271729,1.7059742212295532,1.6832505464553833,1.6453773975372314,1.6335949897766113,1.632752776145935,1.6201286315917969,1.590671181678772,1.6032955646514893,1.7253321409225464,1.7531052827835083,1.7505806684494019,1.83053457736969,1.8094940185546875,1.8852403163909912,1.9231137037277222,1.8566253185272217,1.8094940185546875,1.7505806684494019,1.6706260442733765,1.733747959136963,1.7867697477340698,1.799393892288208,1.7253321409225464,1.7884536981582642,1.8860816955566406,1.9744526147842407,2.0375747680664062,1.9862353801727295,1.957619547843933,2.03589129447937,1.956778883934021,1.9719278812408447,1.956778883934021,1.956778883934021,1.9315297603607178,1.8936564922332764,1.9146971702575684,1.8852403163909912,1.9323716163635254,1.8944984674453735,1.9374209642410278,1.8953397274017334,1.9357377290725708,1.8431590795516968,1.767412781715393,1.7270148992538452,1.6815670728683472,1.5948798656463623,1.6832505464553833,1.7665711641311646,1.6613681316375732,1.578889012336731,1.5570067167282104,1.5999293327331543,1.6672594547271729,1.6411689519882202,1.6159204244613647,1.5511152744293213,1.4888349771499634,1.4055144786834717,1.36259126663208,1.3541747331619263,1.3499670028686523,1.3280845880508423,1.3297677040100098,1.3466004133224487,1.4804185628890991,1.4290797710418701,1.4762108325958252,1.540174126625061,1.5107169151306152,1.472843885421753,1.404672384262085,1.2708542346954346,1.291894555091858,1.3289259672164917,1.3373425006866455,1.2540215253829956,1.2834783792495728,1.3676410913467407,1.3760573863983154,1.4560118913650513,1.5233416557312012,1.5931963920593262,1.6790423393249512,1.760680079460144,1.8052864074707031,1.7253321409225464,1.662209391593933,1.7387977838516235,1.7345894575119019,1.7589964866638184,1.803602933883667,1.7505806684494019,1.6832505464553833,1.5654231309890747,1.614236831665039,1.6504267454147339,1.6874583959579468,1.7169156074523926,1.7505806684494019,1.7169156074523926,1.6495856046676636,1.7009241580963135,1.71859872341156,1.6916664838790894,1.7068160772323608,1.6874583959579468,1.6748337745666504,1.6344363689422607,1.6537930965423584,1.7379554510116577,1.7909780740737915,1.7211235761642456,1.6832505464553833,1.6664180755615234,1.611711859703064,1.6251778602600098,1.5654231309890747,1.590671181678772,1.470319151878357,1.5410151481628418,1.5628981590270996,1.5772056579589844,1.648743987083435,1.6411689519882202,1.6647342443466187,1.71270751953125,1.7547883987426758,1.6133955717086792,1.678200602531433,1.7169156074523926,1.71270751953125,1.561214566230774,1.5149253606796265,1.5149253606796265,1.5065091848373413,1.4837846755981445,1.5216584205627441,1.5780473947525024,1.5654231309890747,1.554481029510498,1.4332877397537231,1.4644278287887573,1.548590064048767,1.599088430404663,1.599088430404663,1.697558045387268,1.7034492492675781,1.60750412940979,1.6201286315917969,1.6361193656921387,1.5570067167282104,1.5620564222335815,1.5570067167282104,1.5713142156600952,1.5654231309890747,1.590671181678772,1.6041375398635864,1.5822550058364868,1.6201286315917969,1.6176034212112427,1.5275497436523438,1.5250248908996582,1.4484370946884155,1.5233416557312012,1.3297677040100098,1.3466004133224487,1.2540215253829956,1.121044635772705,0.7843945026397705,0.7970191240310669,0.7911275029182434,0.7700870633125305,0.7742950320243835,0.7869196534156799,0.8189011812210083,0.8247928023338318,0.8180596828460693,0.8306840658187866,0.8315258622169495,0.8500412106513977,0.8542495965957642,0.892122745513916,0.8736070990562439,0.8879144787788391,0.8332090377807617,0.802910327911377,0.803752064704895,0.803752064704895,0.8121681809425354,0.8332090377807617,0.8205844759941101,0.7919691801071167,0.7574626803398132,0.7566210031509399,0.7574626803398132,0.7465214729309082,0.7153814435005188,0.6951824426651001,0.7145398855209351,0.6943408250808716,0.6733002066612244,0.6665670275688171,0.6497345566749573,0.6387934684753418,0.6733002066612244,0.6665670275688171,0.6926575303077698,0.8584578037261963,0.8752903342247009,0.8576160669326782,0.892122745513916,0.8710820078849792,0.8677154779434204,0.8550912141799927,0.8635074496269226,0.8837063908576965,0.9072719216346741,0.8752903342247009,0.8837063908576965,0.9089550375938416,0.9190548062324524,0.892122745513916,0.902222216129303,0.9257873296737671,0.9712353348731995,1.0183662176132202,1.022574782371521,1.0183662176132202,1.0208913087844849,0.9931176900863647,1.0200499296188354,0.990592896938324,1.001534342765808,1.0099502801895142,1.0099502801895142,1.0133165121078491,1.0099502801895142,1.0107918977737427,1.0250993967056274,1.008266806602478,1.0840132236480713,1.089904546737671,1.0772799253463745,1.0570813417434692,1.0377237796783447,1.0452983379364014,1.0730721950531006,1.056239366531372,1.0629724264144897,1.0419318675994873,1.0604478120803833,1.0688637495040894,1.094112515449524,1.0436151027679443,1.0166832208633423,1.0335156917572021,1.0671807527542114,1.005742073059082,0.9594524502754211,0.9476698637008667,1.0074255466461182,0.9880682229995728,1.117678165435791,1.098320722579956,1.1185200214385986,1.1538679599761963,1.0966377258300781,1.1235696077346802,1.0932711362838745,1.094112515449524,1.0461399555206299,1.0166832208633423,1.0394073724746704,0.9720772504806519,0.9889094233512878,1.0141586065292358,1.0495069026947021,1.0495069026947021,1.0545567274093628,1.0638141632080078,1.0621308088302612,1.0604478120803833,1.0814883708953857,1.0856963396072388,1.0730721950531006,1.0730721950531006,1.0730721950531006,1.0697054862976074,1.0730721950531006,1.110103726387024,1.1681755781173706,1.1673340797424316,1.139560341835022,1.1429270505905151,1.1025290489196777,1.1260945796966553,1.1109451055526733,1.0890631675720215,1.056239366531372,1.0873796939849854,1.110103726387024,1.1446104049682617,1.1193615198135376,1.158918023109436,1.2279313802719116,1.249813437461853,1.2035242319107056,1.182483196258545,1.211940050125122,1.1883745193481445,1.14629328250885,1.1361939907073975,1.1404021978378296,1.1109451055526733,1.154709815979004,1.1159948110580444,1.1319860219955444,1.1361939907073975,1.186691403388977,1.1993155479431152,1.1908994913101196,1.1446104049682617,1.1387187242507935,1.1572345495224,1.1277776956558228,1.1025290489196777,1.1058955192565918,1.070547342300415,1.0654975175857544,1.0730721950531006,1.0814883708953857,1.1025290489196777,1.1109451055526733,1.094112515449524,1.205207347869873,1.2430802583694458,1.316301703453064,1.3701659440994263,1.3886816501617432,1.3423922061920166,1.3802653551101685,1.3886816501617432,1.3996224403381348,1.4560118913650513,1.495567798614502,1.5132420063018799,1.5149253606796265,1.5014594793319702,1.489676833152771,1.450961709022522,1.4299207925796509,1.414771556854248,1.4475953578948975,1.4181386232376099,1.4534868001937866,1.4433870315551758,1.4433870315551758,1.4122470617294312,1.4433870315551758,1.3785820007324219,1.3466004133224487,1.3676410913467407,1.3718490600585938,1.338184118270874,1.3676410913467407,1.3954142332077026,1.403830885887146,1.45180344581604,1.45180344581604,1.4374957084655762,1.472843885421753,1.466111183166504,1.5511152744293213,1.5864636898040771,1.5923551321029663,1.5755223035812378,1.535966157913208,1.5191330909729004,1.5157668590545654,1.4770522117614746,1.4316043853759766,1.3524914979934692,1.403830885887146,1.4602198600769043,1.4307628870010376,1.4307628870010376,1.4156131744384766,1.314618706703186,1.3356592655181885,1.4055144786834717,1.4223463535308838,1.4139302968978882,1.401305913925171,1.4223463535308838,1.4534868001937866,1.4055144786834717,1.360908031463623,1.3466004133224487,1.2750622034072876,1.2969443798065186,1.365115761756897,1.360908031463623,1.386156439781189,1.357541561126709,1.360066294670105,1.359224557876587,1.3457585573196411,1.2834783792495728,1.2876865863800049,1.2506550550460815,1.2371892929077148,1.2346640825271606,1.2035242319107056,1.2169899940490723,1.2876865863800049,1.27422034740448,1.2127816677093506,1.2573878765106201,1.2371892929077148,1.2750622034072876,1.2952609062194824,1.2658042907714844,1.3238763809204102,1.2615960836410522,1.2674875259399414,1.2961030006408691,1.3070439100265503,1.2969443798065186,1.273378849029541,1.3516501188278198,1.5149253606796265,1.4349708557128906,1.5628981590270996,1.5124003887176514,1.5115586519241333,1.499776005744934,1.4795769453048706,1.4644278287887573,1.472843885421753,1.4644278287887573,1.4694772958755493,1.4484370946884155,1.4299207925796509,1.4425455331802368,1.4349708557128906,1.392889380455017,1.3886816501617432,1.3970975875854492,1.3760573863983154,1.3710074424743652,1.3735318183898926,1.3886816501617432,1.466111183166504,1.4139302968978882,1.4475953578948975,1.472843885421753,1.472843885421753,1.4459118843078613,1.5410151481628418,1.5191330909729004,1.5199748277664185,1.5149253606796265,1.4989341497421265,1.5679476261138916,1.5696310997009277,1.5553230047225952,1.5696310997009277,1.5620564222335815,1.5275497436523438,1.5393321514129639,1.5157668590545654,1.5233416557312012,1.498092770576477,1.4922016859054565,1.4366540908813477,1.4189800024032593,1.5065091848373413,1.4795769453048706,1.4450706243515015,1.419821858406067,1.408038854598999,1.4366540908813477,1.3895232677459717,1.4307628870010376,1.4299207925796509,1.45180344581604,1.471160650253296,1.525865912437439,1.5115586519241333,1.5166085958480835,1.5090339183807373,1.5452237129211426,1.5536398887634277,1.548590064048767,1.5418576002120972,1.5502735376358032,1.5527983903884888,1.5107169151306152,1.5073504447937012,1.5393321514129639,1.5334410667419434,1.5376492738723755,1.5140836238861084,1.5561648607254028,1.560373067855835,1.5275497436523438,1.5283912420272827,1.538491129875183,1.5140836238861084,1.493884563446045,1.4821017980575562,1.495567798614502,1.5300743579864502,1.5216584205627441,1.5191330909729004,1.481260061264038,1.4475953578948975,1.472843885421753,1.4593780040740967,1.45180344581604,1.4366540908813477,1.3912066221237183,1.3255597352981567,1.3045192956924438,1.2902113199234009,1.2961030006408691,1.2952609062194824,1.2961030006408691,1.3213515281677246,1.3238763809204102,1.314618706703186,1.3062021732330322,1.3095686435699463,1.2876865863800049,1.3120934963226318,1.3423922061920166,1.3423922061920166,1.3524914979934692,1.3314509391784668,1.2969443798065186,1.2961030006408691,1.3280845880508423,1.3053609132766724,1.2649625539779663,1.2624380588531494,1.2237226963043213,1.2489718198776245,1.2397136688232422,1.2708542346954346,1.2632793188095093,1.2540215253829956,1.2809537649154663,1.2456051111221313,1.2506550550460815,1.2413971424102783,1.227089285850525,1.2371892929077148,1.2456051111221313,1.2624380588531494,1.27422034740448,1.2750622034072876,1.270012378692627,1.2666460275650024,1.2456051111221313,1.2775869369506836,1.3062021732330322,1.291894555091858,1.2254061698913574,1.2262475490570068,1.2868448495864868,1.2716954946517944,1.2952609062194824,1.2961030006408691,1.3196682929992676,1.2876865863800049,1.2792704105377197,1.2582294940948486,1.2624380588531494,1.2514965534210205,1.270012378692627,1.2658042907714844,1.2548630237579346,1.2624380588531494,1.3297677040100098,1.3508083820343018,1.408880352973938,1.4433870315551758,1.4307628870010376,1.408038854598999,1.4273964166641235,1.4307628870010376,1.419821858406067,1.4299207925796509,1.4400207996368408,1.4105638265609741,1.4257131814956665,1.4560118913650513,1.4526453018188477,1.4585365056991577,1.434128999710083,1.4526453018188477,1.450961709022522,1.4585365056991577,1.4686357975006104,1.4753689765930176,1.49640953540802,1.5780473947525024,1.5233416557312012,1.5570067167282104,1.5317575931549072,1.5023010969161987,1.535966157913208,1.5081924200057983,1.49640953540802,1.5292327404022217,1.5578480958938599,1.5923551321029663,1.6790423393249512,1.7026077508926392,1.6739919185638428,1.5923551321029663,1.5755223035812378,1.609187126159668,1.6159204244613647,1.5864636898040771,1.5527983903884888,1.606662631034851,1.60750412940979,1.5931963920593262,1.6108702421188354,1.6394853591918945,1.6218117475509644,1.6159204244613647,1.6369608640670776,1.6840920448303223,1.6748337745666504,1.648743987083435,1.6672594547271729,1.6882998943328857,1.679883599281311,1.7084991931915283,1.8120191097259521,1.9231137037277222,1.8507332801818848,1.8010776042938232,1.8002362251281738,1.9778188467025757,1.9483623504638672,1.877665638923645,1.8515746593475342,1.8431590795516968,1.7286980152130127,1.665576696395874,1.733747959136963,1.807810664176941,1.8263262510299683,1.7968692779541016,1.7749873399734497,1.7758289575576782,1.7724626064300537,1.767412781715393,1.7707794904708862,1.7758289575576782,1.802761435508728,1.802761435508728,1.8221184015274048,1.8094940185546875,1.7867697477340698,1.7892951965332031,1.8069690465927124,1.7800371646881104,1.7690962553024292,1.784245491027832,1.8456844091415405,1.8061275482177734,1.7943451404571533,1.872616171836853,1.8793487548828125,1.8902901411056519,1.8818738460540771,1.8120191097259521,1.792661190032959,1.7909780740737915,1.7800371646881104,1.6453773975372314,1.632752776145935,1.611711859703064,1.6024545431137085,1.5974045991897583,1.6032955646514893,1.6260194778442383,1.6293869018554688,1.6133955717086792,1.60750412940979,1.5721559524536133,1.5729974508285522,1.609187126159668,1.6192870140075684,1.5822550058364868,1.606662631034851,1.6218117475509644,1.6866172552108765,1.6504267454147339,1.6546353101730347,1.6411689519882202,1.6411689519882202,1.609187126159668,1.5923551321029663,1.611711859703064,1.6201286315917969,1.6571599245071411,1.65800142288208,1.663051724433899,1.6436938047409058,1.5746804475784302,1.5856220722198486,1.5654231309890747,1.6184449195861816,1.6335949897766113,1.7059742212295532,1.7068160772323608,1.71270751953125,1.7413227558135986,1.7514219284057617,1.7278565168380737,1.7051326036453247,1.7084991931915283,1.7076573371887207,1.6546353101730347,1.7834042310714722,1.7505806684494019,1.769937515258789,1.7690962553024292,1.7345894575119019,1.6411689519882202,1.847367286682129,1.897864580154419,1.9710863828659058,1.899547815322876,1.9121723175048828,1.8650413751602173,1.8322179317474365,1.833059310913086,1.860832929611206,1.8456844091415405,1.8507332801818848,1.833059310913086,1.8103357553482056,1.847367286682129,1.8111774921417236,1.7598384618759155,1.8187518119812012,1.9954934120178223,2.0283172130584717,1.9710863828659058,2.0131676197052,1.9904435873031616,2.050198793411255,2.068714141845703,2.0594565868377686,2.0645065307617188,2.071239948272705,2.157926082611084,2.146144390106201,2.116687059402466,2.1713926792144775,2.173917531967163,2.167184829711914,2.15960955619812,2.165501356124878,2.1713926792144775,2.1453027725219727,2.160451889038086,2.2050580978393555,2.286695718765259,2.3582334518432617,2.3582334518432617,2.4019980430603027,2.5038349628448486,2.4062066078186035,2.480269432067871,2.5139341354370117,2.45417857170105,2.5282421112060547,2.533292055130005,2.615771532058716,2.737806797027588,2.695725202560425,2.6258704662323,2.7176079750061035,2.7580056190490723,2.7436981201171875,2.72518253326416,2.8211276531219482,2.776521682739258,2.7832536697387695,2.7260236740112305,2.6974081993103027,2.7352821826934814,2.7352821826934814,2.7016167640686035,2.6578519344329834,2.728548765182495,2.7327568531036377,2.752955913543701,2.7613718509674072,2.784937858581543,2.830385684967041,2.8800415992736816,2.959153890609741,2.9852449893951416,3.0046021938323975,2.986085891723633,2.976828098297119,2.961678981781006,2.944005012512207,2.944005012512207,2.9692530632019043,2.9473717212677,2.8985564708709717,2.8766746520996094,2.8657333850860596,2.942321300506592,2.975145101547241,2.8909823894500732,2.8707833290100098,2.9204397201538086,2.88761568069458,2.8169193267822266,2.710033416748047,2.710874557495117,2.7689473628997803,2.772312879562378,2.7352821826934814,2.642703056335449,2.6553268432617188,2.530766725540161,2.4785866737365723,2.721816062927246,2.77567982673645,2.882566213607788,2.93558931350708,2.90360689163208,2.8993990421295166,2.8623673915863037,2.840484619140625,2.804295063018799,2.840484619140625,2.8194446563720703,2.8472177982330322,3.0062849521636963,3.0492076873779297,3.030691146850586,3.041632890701294,3.0601487159729004,3.0500497817993164,3.0887649059295654,3.0163848400115967,3.031533718109131,3.028167247772217,2.971778631210327,2.7874624729156494,2.8110289573669434,2.8446927070617676,2.8017704486846924,2.7537970542907715,2.7647383213043213,2.7016167640686035,2.6485941410064697,2.606513023376465,2.6494359970092773,2.6940414905548096,2.6090385913848877,2.583789110183716,2.629237413406372,2.600621461868286,2.5879971981048584,2.5804226398468018,2.604829788208008,2.6553268432617188,2.7638967037200928,2.8581595420837402,2.8648922443389893,2.8691000938415527,2.921280860900879,3.0020768642425537,2.851426362991333,2.7807297706604004,2.901923418045044,2.986085891723633,2.996185541152954,3.050891160964966,3.113171339035034,3.0618321895599365,3.1308462619781494,3.062673568725586,3.1106460094451904,3.095496416091919,3.022274971008301,3.0391080379486084,2.991135597229004,2.9835612773895264,3.0062849521636963,3.052574396133423,3.181342363357544,3.0786643028259277,2.984403371810913,3.075298547744751,2.9608371257781982,2.9448466300964355,2.831226348876953,2.8287031650543213,2.962520122528076,2.93558931350708,2.945687770843506,2.890141248703003,2.916231393814087,2.8573176860809326,2.874150276184082,2.7697882652282715,2.770630121231079,2.660377264022827,2.6544859409332275,2.5980963706970215,2.5627493858337402,2.5913634300231934,2.5703237056732178,2.577897787094116,2.5980963706970215,2.6528029441833496,2.673001527786255,2.678051710128784,2.719290018081665,2.8152363300323486,3.1401031017303467,3.241940498352051,3.2259490489959717,3.257089853286743,3.29748797416687,3.2436234951019287,3.2267911434173584,3.2208991050720215,3.2032253742218018,3.2562472820281982,3.208275079727173,3.2065911293029785,3.2065911293029785,3.22426700592041,3.2587738037109375,3.294121026992798,3.328627347946167,3.3925909996032715,3.550816535949707,3.539875030517578,3.5827982425689697,3.6274046897888184,3.5255682468414307,3.513784408569336,3.4052155017852783,3.4068984985351562,3.382490634918213,3.4111063480377197,3.4195234775543213,3.5095767974853516,3.463287115097046,3.4094228744506836,3.4540297985076904,3.3631341457366943,3.37070894241333,3.3867006301879883,3.369025230407715,3.4489803314208984,3.3917486667633057,3.4506642818450928,3.432987928390503,3.361450672149658,3.2612974643707275,3.2192163467407227,3.26550555229187,3.2924368381500244,3.403531551361084,3.3488266468048096,3.3749167919158936,3.4590792655944824,3.484328031539917,3.7873129844665527,3.8243446350097656,3.802462100982666,3.9396471977233887,3.9455389976501465,3.900932788848877,3.9556376934051514,3.9556376934051514,3.967420816421509,3.9101901054382324,4.043167591094971,4.096190452575684,4.12312126159668,4.121437072753906,4.095348358154297,3.9539549350738525,3.964895486831665,3.9438557624816895,3.9219729900360107,3.937121868133545,3.9615302085876465,3.999401569366455,3.95479679107666,3.9354407787323,3.93880558013916,3.9876205921173096,3.9850943088531494,3.972470760345459,4.006137371063232,4.041484832763672,4.037275791168213,3.9909868240356445,4.058317184448242,3.995194435119629,4.002769947052002,3.90598201751709,3.7797396183013916,3.6989424228668213,3.656019687652588,3.7283995151519775,3.7536468505859375,3.8192946910858154,3.7847883701324463,3.646761655807495,3.639187812805176,3.539033889770508,3.6585450172424316,3.6678013801574707,3.5499746799468994,3.613938093185425,3.6972596645355225,3.6551780700683594,3.44813871383667,3.507894515991211,3.471703290939331,3.4464545249938965,3.484328031539917,3.3749167919158936,3.325260877609253,3.39848256111145,3.471703290939331,3.318528175354004,3.1914424896240234,3.0870819091796875,3.2335238456726074,3.098021984100342,3.1704020500183105,3.1249542236328125,3.095496416091919,3.125796318054199,3.295804738998413,3.534825563430786,3.3471431732177734,3.2688727378845215,3.3000123500823975,3.204909086227417,3.114854574203491,3.1409459114074707,3.1064388751983643,3.3109538555145264,3.277287721633911,3.1704020500183105,3.319369316101074,3.443929672241211,3.2713961601257324,3.1872341632843018,3.289071559906006,3.3892242908477783,3.438880443572998,3.4380383491516113,3.5533416271209717,3.5020029544830322,3.4060568809509277,3.6114134788513184,3.737657070159912,3.7283995151519775,3.7620644569396973,3.7326080799102783,3.6854782104492188,3.750281572341919,3.909348487854004,3.8807332515716553,3.897566318511963,3.9556376934051514,3.8049871921539307,3.7393407821655273,3.624879837036133,3.6703274250030518,3.672851800918579,3.5541834831237793,3.523042917251587,3.5827982425689697,3.628246545791626,3.669485330581665,3.6762192249298096,3.640869379043579,3.7183005809783936,3.6745355129241943,3.67706036567688,3.76627254486084,3.8378098011016846,3.979203701019287,4.035592555999756,3.970787525177002,4.010343074798584,4.052424430847168,4.037275791168213,4.0709404945373535,4.111339092254639,3.966580390930176,4.038116931915283,4.0608415603637695,3.9733128547668457,3.9253392219543457,3.895040988922119,3.8807332515716553,3.9825708866119385,4.038116931915283,4.059158802032471,4.00697660446167,4.044008731842041,4.038959503173828,4.128171443939209,4.230850696563721,4.352885723114014,4.356252670288086,4.304912090301514,4.290605545043945,4.315011978149414,4.313328742980957,4.3840250968933105,4.283872604370117,4.1811933517456055,4.339420318603516,4.346151828765869,4.283030986785889,4.297338008880615,4.215699672698975,4.233374118804932,4.504378318786621,4.482496738433838,4.463979244232178,4.483337879180908,4.375609397888184,4.400857925415039,4.400857925415039,4.469029903411865,4.437889575958252,4.399174690246582,4.354569435119629,4.305755138397217,4.460613250732422,4.657553195953369,4.767807483673096,4.629780292510986,4.578441619873047,4.6457719802856445,4.717309951782227,4.677752494812012,4.735825061798096,4.7762227058410645,4.836819648742676,4.814096927642822,4.8637518882751465,4.816620349884033,4.746765613555908,4.736666679382324,4.796422004699707,4.7635979652404785,4.667654037475586,4.6331467628479,4.6424055099487305,4.670178413391113,4.649979114532471,4.630621433258057,4.688693046569824,4.695425987243652,4.63819694519043,4.620522975921631,4.6634440422058105,4.670178413391113,4.586856365203857,4.742556571960449,4.766964435577393,4.883110523223877,4.851126670837402,4.855335235595703,4.844394207000732,4.784639358520508,4.715625286102295,4.6331467628479,4.6222052574157715,4.692902565002441,4.5161590576171875,4.397491455078125,4.467347145080566,4.438732147216797,4.496803283691406,4.531309127807617,4.536360263824463,4.460613250732422,4.438732147216797,4.5203680992126465,4.481653690338135,4.505218505859375,4.463979244232178,4.51279354095459,4.5380425453186035,4.5220513343811035,4.522893905639648,4.537201881408691,4.65587043762207,4.570867538452148,4.530467987060547,4.492595672607422,4.3882341384887695,4.408432960510254,4.390758037567139,4.3166961669921875,4.303230285644531,4.358776092529297,4.359618186950684,4.524576663970947,4.561608791351318,4.614631175994873,4.5380425453186035,4.483337879180908,4.558241367340088,4.498486518859863,4.580124378204346,4.654186248779297,4.650820255279541,4.598640441894531,4.60032320022583,4.7080512046813965,5.245008945465088,5.487396240234375,5.45709753036499,5.482346534729004,5.542943000793457,5.5867085456848145,5.5513596534729,5.608590126037598,5.571557521820068,5.733150959014893,5.780282497406006,5.707901954650879,5.687703609466553,5.6944355964660645,5.714635372161865,5.6422553062438965,5.559774875640869,5.731466770172119,5.882959842681885,5.748300552368164,5.692752361297607,5.728100299835205,5.657406330108643,5.5833420753479,5.638889312744141,5.689385414123535,5.654037952423096,5.596806526184082,5.606906890869141,5.632155418395996,5.638889312744141,5.541260242462158,5.49412727355957,5.5513596534729,5.768499374389648,5.933457851409912,5.992371082305908,5.990688800811768,6.244858264923096,6.3424882888793945,6.03445291519165,5.926724910736084,6.024352550506592,6.063067436218262,6.130396842956543,6.224659442901611,6.3424882888793945,6.440115928649902,6.419917583465576,6.2953572273254395,6.130396842956543,6.273475170135498,6.2128777503967285,6.120297431945801,6.2313923835754395,6.271790504455566,6.600024700164795,6.763300895690918,6.74141788482666,6.667354106903076,6.74141788482666,6.743099689483643,6.7296366691589355,6.650521755218506,6.7969651222229,6.719534397125244,6.581509590148926,6.766665935516357,6.808746337890625,6.987173080444336,6.993903160095215,7.280055999755859,7.091533660888672,7.027568817138672,7.140347957611084,7.069651126861572,7.0814337730407715,7.0040059089660645,7.086482524871826,7.014103412628174,7.057867050170898,6.916476726531982,7.0040059089660645,7.071335315704346,6.911426067352295,6.800329685211182,6.854197978973389,6.7919135093688965,6.749833583831787,6.987173080444336,6.657254695892334,6.833996772766113,7.197575569152832,7.413033962249756,6.892909049987793,6.712802410125732,6.849146842956543,6.744783401489258,6.655572414398193,6.561310768127441,6.716169357299805,7.015789031982422,7.231242656707764,7.3086724281311035,7.987021446228027,8.320307731628418,8.199112892150879,7.8136491775512695,8.3556547164917,8.21931266784668,8.439817428588867,8.606460571289062,8.36070442199707,8.424667358398438,8.114949226379395,8.215944290161133,8.446550369262695,8.475165367126465,8.384269714355469,8.729334831237793,8.651906967163086,8.788248062133789,8.990242004394531,9.17203140258789,9.305006980895996,9.454816818237305,9.599576950073242,9.894144058227539,9.559179306030273,9.485113143920898,9.45145034790039,9.695520401000977,9.528882026672363,9.195597648620605,9.547396659851074,9.535614967346191,9.882363319396973,9.926129341125488,9.602943420410156,9.661856651306152,9.766221046447754,9.783050537109375,9.848695755004883,9.828499794006348,9.550762176513672,9.55412769317627,10.107916831970215,9.784736633300781,9.528882026672363,9.668588638305664,9.80829906463623,9.678689956665039,9.968207359313965,9.737604141235352,9.515414237976074,9.591157913208008,9.878996849060059,9.496898651123047,9.392538070678711,8.884195327758789,8.752900123596191,9.161931037902832,9.067667961120605,9.414419174194336,9.2578763961792,8.91954231262207,8.586259841918945,8.301790237426758,8.44150161743164,8.665371894836426,8.944791793823242,9.38748550415039,9.402636528015137,9.670273780822754,9.695520401000977,9.629875183105469,9.746020317077637,10.040589332580566,10.230793952941895,10.099504470825195,9.783050537109375,9.867213249206543,9.687104225158691,9.798201560974121,9.788101196289062,10.261094093322754,10.262776374816895,10.452983856201172,10.343571662902832,10.654973030090332,10.584280014038086,10.469817161560059,10.486650466918945,10.454665184020996,10.149998664855957,10.11801815032959,9.60125732421875,9.513729095458984,9.443035125732422,9.27639389038086,8.798349380493164,8.773101806640625,9.040736198425293,8.552593231201172,8.636757850646973,8.369119644165039,8.301790237426758,8.495366096496582,8.76131820678711,8.823599815368652,8.348920822143555,8.508829116821289,8.36070442199707,8.261394500732422,8.678840637207031,8.84043025970459,8.752900123596191,8.308523178100586,8.29505729675293,8.276540756225586,8.456650733947754,8.456650733947754,8.264758110046387,7.965141773223877,7.7025532722473145,8.017321586608887,7.887711524963379,7.699187755584717,7.741265296936035,7.788399696350098,7.753050804138184,7.92979097366333,7.980288982391357,7.584726810455322,7.130247592926025,7.194213390350342,7.33897066116333,7.613340377807617,7.298573970794678,7.184114456176758,7.29352331161499,7.889395236968994,7.785034656524658,7.939892292022705,8.256342887878418,7.911275386810303,8.17218017578125,7.907909870147705,8.446550369262695,9.087869644165039,9.064302444458008,8.917861938476562,9.08955192565918,8.734386444091797,8.70408821105957,9.370655059814453,9.370655059814453,9.493531227111816,9.496898651123047,9.436301231384277,9.316790580749512,9.037369728088379,9.289856910705566,9.180447578430176,9.239357948303223,9.40095329284668,9.537296295166016,9.60125732421875,9.533928871154785,9.353821754455566,9.232626914978027,9.293224334716797,9.421151161193848,9.456498146057129,9.278076171875,9.195597648620605,9.264610290527344,9.491849899291992,9.087869644165039,8.879146575927734,9.072720527648926,8.78320026397705,8.59467601776123,8.623290061950684,9.10638427734375,9.190546989440918,9.252826690673828,9.333622932434082,9.067667961120605,8.786565780639648,8.682207107543945,8.55764389038086,8.222678184509277,8.310206413269043,8.332088470458984,8.465068817138672,8.279908180236816,8.348920822143555,8.274856567382812,8.151981353759766,7.975241184234619,8.005539894104004,7.5746259689331055,7.7143354415893555,7.512347221374512,7.155498027801514,7.224510192871094,7.492147445678711,8.069500923156738,7.887711524963379,7.852361679077148,8.069500923156738,7.645321369171143,7.699187755584717,7.641956329345703,7.746318817138672,7.327188491821289,7.209359645843506,6.800329685211182,6.859243869781494,6.802014350891113,6.527644157409668,6.625274181365967,6.852510452270508,6.6286396980285645,6.551209449768066,6.611807346343994,6.778448581695557,6.936673641204834,7.195894718170166,7.29352331161499,7.616708278656006,7.246394157409668,7.312039375305176,7.4450154304504395,7.163912296295166,6.992222785949707,6.830629348754883,6.985489368438721,6.904691696166992,6.818845748901367,6.704387664794922,6.637056350708008,7.2211456298828125,7.200944900512695,6.972023010253906,7.443331718444824,7.704238414764404,7.599875450134277,7.441649436950684,7.478681564331055,7.2733259201049805,7.436601161956787,7.413033962249756,7.325506210327148,7.3187713623046875,7.433233737945557,7.281738758087158,7.256493091583252,7.254809379577637,7.421451091766357,7.384420394897461,7.638589382171631,7.389469146728516,7.394519329071045,7.344018936157227,7.453432083129883,7.330554008483887,7.197575569152832,7.187477111816406,6.936673641204834,6.5478434562683105,6.746469020843506,6.329020023345947,6.4788312911987305,6.345854759216309,6.106832504272461,5.881276607513428,5.824047565460205,6.066434383392334,6.086633682250977,5.756716728210449,5.75839900970459,6.066434383392334,6.0277204513549805,5.938506126403809,5.7415666580200195,5.175994396209717,5.085100173950195,4.896575450897217,4.898258686065674,5.6422553062438965,5.110347747802734,4.667654037475586,5.186094760894775,5.359469890594482,5.5867085456848145,5.1271796226501465,4.7518157958984375,4.556559085845947,4.331002712249756,4.243473052978516,4.866275310516357,4.953805446624756,4.953805446624756,4.610422611236572,4.539726734161377,4.671019554138184,4.255256652832031,4.007818698883057,4.224957466125488,4.120596885681152,3.940488576889038,3.709883213043213,4.179510593414307,3.918606996536255,3.8293943405151367,3.7384986877441406,3.4607620239257812,2.945687770843506,3.0264840126037598,3.401848316192627,3.479278802871704,3.7031493186950684,3.6779026985168457,3.257089853286743,3.1998586654663086,3.1729273796081543,3.3967998027801514,3.5802741050720215,4.208125591278076,3.9101901054382324,4.0549492835998535,3.844543695449829,4.06168270111084,3.891674518585205,4.3242692947387695,4.320903778076172,4.105447292327881,4.1407952308654785,3.895040988922119,3.7334487438201904,3.923656463623047,3.895040988922119,3.694734573364258,3.7267160415649414,3.6459202766418457,3.9034576416015625,4.011186122894287,3.9590063095092773,3.8058295249938965,4.305755138397217,4.398333549499512,4.287239074707031,4.147528648376465,3.9438557624816895,4.011186122894287,4.154261589050293,3.8798911571502686,4.112180709838867,4.095348358154297,4.344470024108887,4.470712661743164,4.438732147216797,4.736666679382324,4.430315017700195,4.17109489440918,4.285555839538574,4.312488079071045,4.3747663497924805,4.563292503356934,4.714783191680908,4.615471839904785,4.527944087982178,4.462296962738037,4.543093204498291,4.41853141784668,4.211492538452148,4.186243534088135,4.482496738433838,4.490912437438965,4.413480758666992,4.605372428894043,4.765281677246094,4.54477596282959,4.531309127807617,4.391600131988525,4.373084545135498,4.595273494720459,3.9489052295684814,3.7671139240264893,3.8546433448791504,4.243473052978516,4.251889705657959,4.275454998016357,4.31921911239624,4.108814239501953,4.199709892272949,4.179510593414307,4.27882194519043,4.182876110076904,4.4808125495910645,4.553192138671875,4.517843723297119,4.411799907684326,4.684486389160156,4.556559085845947,4.716466903686523,4.746765613555908,5.06658411026001,5.012719631195068,4.8174614906311035,4.923506736755371,5.10698127746582,5.45709753036499,5.435215950012207,5.30055570602417,5.369568824768066,4.999253749847412,4.852810382843018,4.780430793762207,5.016086101531982,5.026185035705566,5.133913516998291,5.2702555656433105,5.130547046661377,4.994202613830566,5.064899921417236,5.076683044433594,4.938656330108643,4.938656330108643,4.896575450897217,4.630621433258057,4.529627799987793,4.398333549499512,4.487545013427734,4.41853141784668,4.31921911239624,4.371400833129883,4.455564022064209,4.423582077026367,4.346151828765869,4.455564022064209,3.7671139240264893,3.795729160308838,3.932072639465332,3.704833745956421,3.960688829421997,4.199709892272949,4.342785358428955,4.093664646148682,4.06841516494751,4.115545749664307,4.021285057067871,4.095348358154297,4.208125591278076,4.199709892272949,4.14247989654541,4.059998989105225,3.984252452850342,3.869792938232422,3.911874532699585,3.8378098011016846,3.8630595207214355,3.6964175701141357,3.6795852184295654,3.6745355129241943,3.7384986877441406,3.7317655086517334,3.7317655086517334,3.704833745956421,3.7805802822113037,3.5466089248657227,3.5415589809417725,3.443929672241211,3.5247273445129395,3.4826455116271973,3.4405641555786133,3.539875030517578,3.640869379043579,3.6425538063049316,3.7283995151519775,3.6964175701141357,3.7603814601898193,3.8580093383789062,3.975837469100952,4.022968292236328,4.065048694610596,3.960688829421997,3.8378098011016846,3.6812689304351807,3.615621328353882,3.6846354007720947,3.847910165786743,4.110498428344727,4.065048694610596,4.127330303192139,4.2350568771362305,4.066732883453369,4.157629489898682,4.315852165222168,4.431997299194336,4.4505133628845215,4.223275184631348,4.130697250366211,4.2384233474731445,3.940488576889038,3.893357515335083,3.797412633895874,3.7755303382873535,3.797412633895874,3.8748419284820557,3.950587749481201,4.006137371063232,3.9253392219543457,3.9489052295684814,4.031383991241455,4.049900531768799,4.196342945098877,4.216543197631836,4.211492538452148,4.157629489898682,4.307436943054199,4.265355587005615,4.346151828765869,4.342785358428955,4.50942850112915,4.423582077026367,4.416848182678223,4.487545013427734,4.415165424346924,4.383183479309082,4.411799907684326,4.50942850112915,4.455564022064209,4.37981653213501,4.322585582733154,4.381500720977783,4.4808125495910645,4.416848182678223,4.607056617736816,4.5380425453186035,4.52121114730835,4.602005958557129,4.740033149719238,4.686168670654297,4.667654037475586,4.740033149719238,4.317537784576416,4.265355587005615,4.248523235321045,4.1694111824035645,4.0532660484313965,4.1407952308654785,4.078515529632568,4.132379055023193,4.088615894317627,4.07178258895874,4.036435127258301,3.9960367679595947,4.07178258895874,4.145845413208008,4.292288780212402,4.2384233474731445,4.112180709838867,4.144163608551025,3.9876205921173096,4.107129096984863,4.034750461578369,4.0549492835998535,4.123962879180908,4.290605545043945,4.31921911239624,4.255256652832031,4.309119701385498,4.261990070343018,4.108814239501953,4.012868881225586,3.6812689304351807,3.593738555908203,3.5903730392456055,3.691368818283081,3.593738555908203,3.5045275688171387,3.5651237964630127,3.656019687652588,3.750281572341919,3.75533127784729,3.7772138118743896,3.8125627040863037,3.7839465141296387,3.807511329650879,3.7401819229125977,3.704833745956421,3.704833745956421,3.743548631668091,3.7317655086517334,3.7317655086517334,3.6930510997772217,3.8546433448791504,3.9590063095092773,4.0448503494262695,3.443929672241211,3.4153146743774414,3.4203648567199707,3.4961113929748535,3.4994773864746094,3.4506642818450928,3.4506642818450928,3.5028438568115234,3.452345848083496,3.43719744682312,3.3715498447418213,3.354717493057251,3.305903673171997,3.356401205062866,3.3429343700408936,3.3277862071990967,3.354717493057251,3.4052155017852783,3.452345848083496,3.3833329677581787,3.3917486667633057,3.3143198490142822,3.167876720428467,3.2267911434173584,3.2587738037109375,3.2267911434173584,3.1964924335479736,3.2453064918518066,3.2688727378845215,3.2503557205200195,3.211641311645508,3.176293134689331,3.1746110916137695,2.9473717212677,2.895190715789795,2.944005012512207,2.944005012512207,3.0046021938323975,2.994502305984497,3.0433168411254883,3.108962059020996,3.039949655532837,3.076982259750366,3.257089853286743,3.2335238456726074,3.26550555229187,3.2671899795532227,3.3429343700408936,3.5617575645446777,3.5533416271209717,3.635820150375366,3.73681640625,3.6543362140655518,3.666118621826172,3.7031493186950684,3.664435863494873,3.672851800918579,3.6880009174346924,3.7704806327819824,3.8108789920806885,3.788996934890747,3.817612409591675,3.891674518585205,3.9219729900360107,3.950587749481201,3.9825708866119385,4.031383991241455,4.110498428344727,4.176144123077393,4.2586236000061035,4.275454998016357,4.231691837310791,4.2131757736206055,4.245157241821289,4.285555839538574,4.130697250366211,4.160994529724121,4.206442356109619,4.091981887817383,4.231691837310791,4.16436243057251,4.125647068023682,3.9017744064331055,3.80077862739563,3.9219729900360107,3.8613767623901367,3.895040988922119,3.817612409591675,3.6779026985168457,3.708200216293335,3.6038384437561035,3.5802741050720215,3.4708619117736816,3.585322380065918,3.581956148147583,3.6880009174346924,3.6459202766418457,3.8681092262268066,3.836127758026123,3.6795852184295654,3.7250325679779053,3.817612409591675,3.664435863494873,3.5583908557891846,3.533142328262329,3.533142328262329,3.5735394954681396,3.6459202766418457,3.6829516887664795,3.486011505126953,3.305903673171997,3.2587738037109375,3.2335238456726074,3.1746110916137695,3.169560432434082,3.179658889770508,3.092130422592163,3.1156961917877197,3.156094789505005,3.0837152004241943,3.162827491760254,3.209958791732788,3.075298547744751,3.097180128097534,3.156094789505005,3.1729273796081543,3.2032253742218018,3.2520389556884766,3.2840213775634766,3.2840213775634766,3.2857046127319336,3.1897597312927246,3.26550555229187,3.332836151123047,3.3092706203460693,3.3648183345794678,3.4506642818450928,3.516310214996338,3.4153146743774414,3.3681840896606445,3.3227362632751465,3.3749167919158936,3.5533416271209717,3.477595567703247,3.5785903930664062,3.5567073822021484,3.529775381088257,3.5280919075012207,3.4557130336761475,3.3429343700408936,3.3176863193511963,3.294121026992798,3.3378851413726807,3.3698673248291016,3.4944283962249756,3.208275079727173,3.166193723678589,3.1005470752716064,3.0870819091796875,3.1005470752716064,3.0870819091796875,3.085397958755493,3.0079681873321533,3.0180678367614746,3.076982259750366,3.114013433456421,3.1998586654663086,3.156094789505005,3.125796318054199,3.093813419342041,3.071932315826416,3.1392621994018555,3.132528066635132,3.129162073135376,3.26550555229187,3.260455846786499,3.2924368381500244,3.278970718383789,3.2823379039764404,3.289071559906006,3.353034257888794,3.3362021446228027,3.3463010787963867,3.31600284576416,3.3176863193511963,3.3665010929107666,3.3479838371276855,3.4068984985351562,3.401848316192627,3.353034257888794,3.37996768951416,3.428781032562256,3.332836151123047,3.2402572631835938,3.167876720428467,3.0837152004241943,3.075298547744751,3.1005470752716064,3.1914424896240234,3.204909086227417,3.220057964324951,3.2368898391723633,3.26550555229187,3.262139081954956,3.2671899795532227,3.307586193084717,3.2503557205200195,3.295804738998413,3.290754795074463,3.3580846786499023,3.3648183345794678,3.4557130336761475,3.39848256111145,3.390065908432007,3.5516579151153564,3.5062105655670166,3.487694025039673,3.5095767974853516,3.534825563430786,3.433831214904785,3.3867006301879883,3.430464267730713,3.401848316192627,3.4254150390625,3.4506642818450928,3.3867006301879883,3.353034257888794,3.4119484424591064,3.5600743293762207,3.5903730392456055,3.5769073963165283,3.608888864517212,3.5886902809143066,3.6425538063049316,3.743548631668091,3.689685344696045,3.6593856811523438,3.6290876865386963,3.6543362140655518,3.6476049423217773,3.5785903930664062,3.6425538063049316,3.6526525020599365,3.7401819229125977,3.745232343673706,3.790679454803467,3.788996934890747,3.8630595207214355,3.8512766361236572,3.8563272953033447,3.7873129844665527,3.6846354007720947,3.472545623779297,3.4961113929748535,3.484328031539917,3.39848256111145,3.479278802871704,3.467495918273926,3.428781032562256,3.428781032562256,3.443929672241211,3.5365095138549805,3.5179929733276367,3.5499746799468994,3.5449252128601074,3.5415589809417725,3.5466089248657227,3.5314583778381348,3.5466089248657227,3.4590792655944824,3.3362021446228027,3.2823379039764404,3.3749167919158936,3.390065908432007,3.3698673248291016,3.31600284576416,3.428781032562256,3.4136321544647217,3.344618558883667,3.373234510421753,3.4119484424591064,3.385016679763794,3.3580846786499023,3.3126370906829834,3.3126370906829834,3.2840213775634766,3.341252088546753,3.3580846786499023,3.319369316101074,3.31600284576416,3.3883824348449707,3.3749167919158936,3.3176863193511963,3.3362021446228027,3.326103448867798,3.295804738998413,3.3277862071990967,3.3362021446228027,3.4557130336761475,3.4573960304260254,3.5314583778381348,3.5280919075012207,3.5668084621429443,3.5381925106048584,3.5533416271209717,3.657702684402466,3.656019687652588,3.6981005668640137,3.757014036178589,3.809194564819336,3.790679454803467,3.8580093383789062,3.799095630645752,3.9691035747528076,4.022968292236328,4.0448503494262695,4.007818698883057,3.9977192878723145,4.006137371063232,4.268723011016846,4.277140140533447,4.443780422210693,4.400016784667969,4.470712661743164,4.435364246368408,4.467347145080566,4.458930969238281,4.425264835357666,4.413480758666992,4.410116195678711,4.322585582733154,4.339420318603516,4.352885723114014,4.322585582733154,4.354569435119629,4.285555839538574,4.28892183303833,4.339420318603516,4.342785358428955,4.3646674156188965,4.497644901275635,4.457246780395508,4.435364246368408,4.490912437438965,4.598640441894531,4.692902565002441,4.65587043762207,4.649137020111084,4.671019554138184,4.671019554138184,4.748449325561523,4.7097344398498535,4.623888969421387,4.5885396003723145,4.499328136444092,4.472395896911621,4.406749725341797,4.421898365020752,4.460613250732422,4.420215129852295,4.41853141784668,4.448829650878906,4.396649360656738,4.410116195678711,4.4505133628845215,4.511110782623291,4.630621433258057,4.467347145080566,4.420215129852295,4.396649360656738,4.341103553771973,4.435364246368408,4.3747663497924805,4.48922872543335,4.532992839813232,4.6121063232421875,4.596956253051758,4.5818071365356445,4.519527435302734,4.368034839630127,4.176144123077393,4.078515529632568,4.011186122894287,3.970787525177002,3.9421727657318115,3.9909868240356445,3.918606996536255,3.9253392219543457,3.950587749481201,3.9775209426879883,3.999401569366455,3.9556376934051514,3.9657373428344727,3.9691035747528076,3.889991044998169,3.8563272953033447,3.8462274074554443,3.6829516887664795,3.7250325679779053,3.4607620239257812,3.595423698425293,3.4573960304260254,3.608888864517212,3.487694025039673,3.5264089107513428,3.6004724502563477,3.443929672241211,3.607205867767334,3.6307713985443115,3.6375036239624023,3.80077862739563,3.930389881134033,3.7873129844665527,3.8344430923461914,3.8883090019226074,3.932072639465332,4.028017997741699,3.878209352493286,3.7283995151519775,3.839494228363037,3.9085075855255127,3.8563272953033447,3.893357515335083,3.9085075855255127,3.9000911712646484,4.024652004241943,4.147528648376465,4.189610481262207,4.078515529632568,4.036435127258301,3.9455389976501465,3.8058295249938965,3.788996934890747,3.9741547107696533,4.019601821899414,3.9590063095092773,4.038116931915283,3.8883090019226074,3.8664259910583496,4.004453182220459,4.017918109893799,4.049900531768799,4.095348358154297,4.137428283691406,4.19465970993042,4.317537784576416,4.245157241821289,4.2350568771362305,4.080199718475342,4.20475959777832,4.186243534088135,4.218226909637451,4.214858531951904,4.305755138397217,4.309119701385498,4.214858531951904,4.361301422119141,4.410116195678711,4.304070472717285,4.214858531951904,4.224957466125488,4.347835063934326,4.3242692947387695,4.283872604370117,4.315852165222168,4.19465970993042,4.1407952308654785,4.236740589141846,4.147528648376465,3.9657373428344727,3.790679454803467,3.691368818283081,3.7805802822113037,3.8243446350097656,3.7755303382873535,3.721665859222412,3.620671510696411,3.7637476921081543,3.8293943405151367,3.891674518585205,3.932072639465332,3.9085075855255127,3.9859366416931152,3.9287068843841553,3.9876205921173096,3.967420816421509,4.073464870452881,4.159311771392822,4.0515828132629395,3.9539549350738525,3.989304304122925,3.9287068843841553,3.815927505493164,3.950587749481201,3.962371587753296,4.004453182220459,4.0263352394104,4.0263352394104,4.0515828132629395,4.098714828491211,4.06168270111084,4.004453182220459,4.06168270111084,4.251889705657959,4.186243534088135,4.038116931915283,4.078515529632568,4.103764057159424,4.070099353790283,3.957322120666504,3.9101901054382324,4.043167591094971,4.1811933517456055,4.132379055023193,4.167727470397949,4.166044235229492,4.208125591278076,4.157629489898682,4.093664646148682,3.9960367679595947,3.932072639465332,3.923656463623047,3.916924238204956,3.979203701019287,3.940488576889038,3.9943530559539795,4.122279644012451,4.0532660484313965,3.8512766361236572,3.8613767623901367,3.8681092262268066,3.839494228363037,3.903881311416626,3.927602767944336,3.9479353427886963,3.8920199871063232,3.946242094039917,3.8513545989990234,3.8971028327941895,3.9530186653137207,3.859825849533081,4.039432525634766,4.044515609741211,4.093653678894043,4.030961036682129,4.049598217010498,4.102125644683838,4.049598217010498,4.027571201324463,4.030961036682129,3.9818224906921387,4.034348964691162,3.9919891357421875,4.058070182800293,4.068237781524658,4.1800665855407715,3.9242146015167236,4.002155780792236,4.032656669616699,4.025876045227051,3.980128526687622,3.8276329040527344,3.700554132461548,3.8056063652038574,3.734441041946411,3.7191922664642334,3.681915044784546,3.7022488117218018,3.629389762878418,3.603973865509033,3.653110980987549,3.5971946716308594,3.6768314838409424,3.753080129623413,3.776801586151123,3.776801586151123,3.792050838470459,3.790356397628784,3.775106906890869,3.8259384632110596,3.8259384632110596,3.842883586883545,3.8564374446868896,3.873382091522217,3.8581318855285645,3.808994770050049,3.698859453201294,3.5734739303588867,3.5768630504608154,3.542975664138794,3.5700857639312744,3.444699764251709,3.537891387939453,3.493837594985962,3.5311152935028076,3.1380155086517334,3.2312076091766357,3.2159574031829834,3.2261242866516113,3.232901096343994,3.273888349533081,3.333662509918213,3.3661108016967773,3.357571601867676,3.275597333908081,3.2790122032165527,3.2790122032165527,3.3370778560638428,3.3046295642852783,3.210700035095215,3.2499799728393555,3.1218934059143066,3.171420097351074,3.0928597450256348,3.0296714305877686,3.0450406074523926,3.1116456985473633,3.1372628211975098,3.0979835987091064,2.998929977416992,3.021131992340088,2.9357411861419678,2.9852681159973145,3.043333053588867,3.041625499725342,3.1355557441711426,3.0706582069396973,3.1372628211975098,3.120185613632202,3.09627628326416,2.9920992851257324,2.9972219467163086,2.9391562938690186,2.920369863510132,2.8742592334747314,2.8298556804656982,2.858889102935791,2.8862144947052,2.869136095046997,2.7837445735931396,2.7564196586608887,2.686398506164551,2.693230628967285,2.727386951446533,2.7564196586608887,2.7359261512756348,2.7359261512756348,2.7444653511047363,2.689814805984497,2.715432643890381,2.7342185974121094,2.8708431720733643,2.85718035697937,2.8742592334747314,3.0296714305877686,3.055288314819336,2.95111083984375,2.9118313789367676,3.0706582069396973,3.171420097351074,3.3285388946533203,3.3285388946533203,3.2089922428131104,3.2277774810791016,3.187971830368042,3.141242265701294,3.139511823654175,3.2208545207977295,3.316044330596924,3.302199125289917,3.5323829650878906,3.556612491607666,3.644878625869751,3.7487220764160156,3.7366063594818115,3.7677602767944336,3.8196816444396973,3.8733341693878174,4.006598472595215,3.857757806777954,3.8819870948791504,3.9512150287628174,3.9356391429901123,3.8594865798950195,3.8300652503967285,3.6137266159057617,3.655264139175415,3.620649576187134,3.6344945430755615,3.6760306358337402,3.6916096210479736,3.6864168643951416,3.871603012084961,3.9944839477539062,4.023905277252197,4.1519775390625,3.973714828491211,3.9564077854156494,3.9408321380615234,3.942561388015747,3.971985101699829,3.9702537059783936,4.056788444519043,4.001406192779541,4.015253067016602,3.9979445934295654,4.029097080230713,4.10524845123291,3.9806370735168457,3.9512150287628174,4.084479331970215,4.12082576751709,4.10524845123291,4.13986349105835,4.049866199493408,3.8975634574890137,3.826603889465332,3.996213912963867,4.025636672973633,4.063713073730469,4.240243911743164,4.421968936920166,4.486006259918213,4.581195831298828,4.686768531799316,4.685037612915039,4.685037136077881,4.660582065582275,4.618658065795898,4.578479290008545,4.58546781539917,4.512100696563721,4.520833969116211,4.536556720733643,4.653594493865967,4.768886566162109,4.793342113494873,4.840505599975586,4.86146879196167,4.8230390548706055,4.805569648742676,4.807315826416016,4.8422532081604,4.812556743621826,4.564505100250244,4.466680526733398,4.468429088592529,4.347896575927734,4.3094658851623535,4.28501033782959,4.382833957672119,4.48240327835083,4.255313873291016,4.332174777984619,4.323441028594971,4.050932884216309,3.949615955352783,3.9810590744018555,4.06141471862793,4.0194902420043945,4.045691967010498,4.029970169067383,4.103338241577148,4.066654205322266,4.073641300201416,4.043944835662842,4.099844455718994,4.141768455505371,4.15399694442749,4.195920944213867,4.12954044342041,4.052680015563965,4.312960147857666,4.410782814025879,4.683289527893066,4.402048587799072,4.438733100891113,4.552277565002441,4.576733112335205,4.515594005584717,4.547036170959473,4.498125076293945,4.431745529174805,4.454452991485596,4.424757480621338,4.319946765899658,4.335667610168457,4.298984527587891,4.330427646636963,4.409036636352539,4.377592086791992,4.247776031494141,4.1576972007751465,4.291930675506592,4.31135892868042,4.334321022033691,4.357281684875488,4.461489677429199,4.5003461837768555,4.530372142791748,4.487982273101807,4.495046138763428,4.542734622955322,4.457956790924072,4.495046138763428,4.457956790924072,4.532138824462891,4.482683181762695,4.655773639678955,4.671669960021973,4.940135955810547,5.256290912628174,5.34106969833374,5.342835903167725,5.2792510986328125,5.2916154861450195,5.344601631164551,5.277485370635986,5.282784461975098,5.595406532287598,5.655458927154541,5.542419910430908,5.704911708831787,5.787923812866211,5.77202844619751,5.780860900878906,5.743768692016602,5.862106800079346,6.045793533325195,6.047561168670654,6.114677429199219,6.105844497680664,6.164132595062256,6.135870933532715,6.4131693840026855,6.561532497406006,6.5685954093933105,6.5862603187561035,6.55976676940918,6.550934314727783,6.778779029846191,6.7593512535095215,6.8246989250183105,6.886518478393555,6.720492839813232,7.022517681121826,6.845894813537598,6.496181011199951,6.4025726318359375,6.360182762145996,5.671355247497559,5.602471828460693,5.620133399963379,5.9168596267700195,5.905284404754639,6.126109600067139,6.320220947265625,6.208028316497803,6.165287017822266,6.544607162475586,6.231177806854248,6.717348575592041,6.516114711761475,6.6835126876831055,6.947079658508301,6.8562541007995605,6.849132537841797,6.861597537994385,7.290782928466797,7.262289047241211,7.105573654174805,7.134068965911865,7.191056251525879,7.278315544128418,7.484893798828125,7.5169501304626465,7.509823799133301,7.547221660614014,7.655855655670166,7.591745376586914,7.602429389953613,7.55434513092041,7.586400985717773,7.687911510467529,7.743115425109863,7.807225704193115,7.743115425109863,7.769828796386719,7.7395548820495605,7.66119909286499,7.55434513092041,7.700375556945801,7.908735275268555,8.156272888183594,8.083257675170898,8.3539457321167,8.736828804016113,8.900666236877441,8.97368049621582,8.955870628356934,8.724361419677734,8.526688575744629,8.635322570800781,8.720802307128906,8.811623573303223,8.768882751464844,8.670937538146973,8.492852210998535,8.47326374053955,8.494632720947266,8.590799331665039,8.480384826660156,9.244367599487305,9.192724227905273,9.328069686889648,8.792033195495605,8.8864164352417,9.071758270263672,8.99117374420166,8.948200225830078,8.889104843139648,9.168457984924316,8.883732795715332,8.971478462219238,9.014457702636719,8.874781608581543,8.855082511901855,9.392295837402344,9.33320426940918,9.422738075256348,9.200689315795898,9.283062934875488,8.85150146484375,8.919548988342285,9.141596794128418,9.09682846069336,9.030572891235352,8.89089584350586,8.89089584350586,9.170248031616211,9.01087474822998,8.921338081359863,9.078922271728516,8.878360748291016,8.831803321838379,8.957152366638184,9.29201602935791,9.232921600341797,9.272316932678223,9.18636417388916,9.25083065032959,9.431692123413086,9.648367881774902,9.786252975463867,9.805953025817871,9.754019737243652,9.81311321258545,9.827439308166504,9.74327564239502,9.929512023925781,9.888325691223145,9.816697120666504,9.857881546020508,9.902649879455566,10.128280639648438,10.036953926086426,9.637624740600586,9.934883117675781,9.916973114013672,10.199908256530762,10.312723159790039,10.284070014953613,10.122908592224121,9.856091499328613,9.524807929992676,9.390503883361816,8.738685607910156,8.92850112915039,8.756593704223633,8.641984939575195,8.554243087768555,8.640195846557617,8.459197998046875,8.275496482849121,8.243082046508789,8.127819061279297,8.118813514709473,8.208861351013184,8.243082046508789,8.14222526550293,8.214262962341309,8.516828536987305,8.664507865905762,8.82119369506836,8.992287635803223,8.98148250579834,8.869821548461914,9.098546028137207,9.179588317871094,9.069729804992676,8.832002639770508,8.87342357635498,8.871621131896973,8.941858291625977,8.86801815032959,8.675315856933594,7.949521064758301,8.167437553405762,8.09900188446045,8.198057174682617,8.162036895751953,6.5393548011779785,6.6582183837890625,6.798696041107178,6.7806854248046875,6.8815388679504395,7.068842887878418,6.888744354248047,6.577174663543701,6.721253395080566,6.492527961730957,6.316033363342285,6.359257698059082,6.316033363342285,6.09271240234375,6.114321708679199,6.260201454162598,6.366458892822266,6.393473148345947,6.559165000915527,6.438499450683594,6.575374126434326,6.458309650421143,6.413286209106445,6.508738040924072,6.411484241485596,6.418688774108887,6.404280662536621,6.492527961730957,6.9283647537231445,6.856326103210449,6.708646774291992,6.719452381134033,6.697839736938477,6.72665548324585,6.978792190551758,6.967987537384033,6.937370300292969,6.9355692863464355,6.931967258453369,6.9337687492370605,6.743031978607178,7.0809102058410645,7.220783233642578,6.973732948303223,6.832043170928955,6.982815265655518,6.870189666748047,6.922870635986328,6.864739894866943,7.066376209259033,6.781179428100586,7.378824234008789,7.466017723083496,7.734866619110107,7.878374099731445,8.0636625289917,7.782098293304443,7.905622959136963,7.945589542388916,7.843861103057861,7.485998153686523,7.360657215118408,7.478735446929932,7.529597282409668,7.400622844696045,7.533231258392334,7.442401885986328,7.678553104400635,7.249847412109375,7.304345607757568,7.151754379272461,7.3279595375061035,7.329777717590332,7.208065986633301,7.131772518157959,7.251663684844971,6.9301347732543945,6.841124534606934,6.510511875152588,6.543209075927734,6.6413044929504395,6.688534259796143,6.875638961791992,6.62313985824585,6.51596212387085,6.579541206359863,6.717599391937256,6.6176886558532715,6.710333347320557,6.699433326721191,6.98099946975708,6.773911476135254,6.941032886505127,6.9337687492370605,6.875638961791992,6.699716567993164,6.701548099517822,6.827993392944336,6.723538875579834,6.831657886505127,6.692386150360107,6.833490371704102,6.915956020355225,6.652071475982666,6.7785162925720215,6.912289619445801,7.383247375488281,7.330105781555176,7.322775363922119,7.350264549255371,7.403407096862793,7.374086856842041,7.368588924407959,7.434560298919678,7.394244194030762,7.416234493255615,7.421731948852539,7.489535808563232,7.6526288986206055,7.621476173400879,7.630640029907227,7.6581268310546875,7.656294822692871,7.557337760925293,7.656294822692871,7.51702356338501,7.6123151779174805,7.559170722961426,7.848709583282471,7.8523736000061035,8.079607009887695,8.195058822631836,8.44794750213623,8.37098217010498,8.444281578063965,7.958661079406738,7.905519962310791,7.691112518310547,7.553671836853027,7.639802932739258,7.573830604553223,7.604984760284424,7.489535808563232,7.458381175994873,7.630640029907227,7.5005316734313965,7.575662136077881,7.6654582023620605,7.264135360717773,7.449219226837158,7.491369247436523,7.573830604553223,7.419900417327881,7.861536979675293,7.771744728088379,7.837715148925781,7.878031253814697,7.911017417907715,7.792830944061279,8.079062461853027,8.038434028625488,8.206480026245117,8.354209899902344,8.176932334899902,7.970108509063721,7.966414451599121,8.117839813232422,8.053210258483887,8.03473949432373,8.282191276550293,8.128920555114746,8.167699813842773,8.010734558105469,8.010734558105469,7.826071262359619,7.971954822540283,7.766979217529297,7.763284683227539,7.766979217529297,7.60816764831543,7.456742763519287,7.549075126647949,7.471513748168945,7.305317401885986,7.20375394821167,7.3200907707214355,7.072639465332031,7.074487209320068,6.869510173797607,6.869510173797607,7.1021857261657715,7.244378566741943,7.3607177734375,7.508447647094727,7.517682075500488,7.497367858886719,7.619245529174805,7.76143741607666,7.720811367034912,7.576773166656494,7.669106960296631,7.77067232131958,7.896241664886475,7.8870110511779785,7.890702247619629,7.947951316833496,8.260031700134277,8.067978858947754,7.892549514770508,7.848228931427002,8.016274452209473,8.21017074584961,8.19909381866455,8.143692016601562,8.128920555114746,8.053210258483887,8.10122013092041,7.044376850128174,7.02577018737793,6.9587883949279785,6.921576023101807,7.035074234008789,6.666668891906738,6.6127095222473145,6.811798095703125,6.897387981414795,6.962508678436279,6.547585964202881,6.618291854858398,6.201508045196533,6.3094258308410645,6.009862422943115,6.127082824707031,5.939157962799072,6.082427978515625,6.158712863922119,6.4192023277282715,6.34849739074707,6.4433913230896,6.212672710418701,6.261049270629883,6.261049270629883,6.294539451599121,6.288959503173828,6.288959503173828,6.460137367248535,6.268491744995117,6.195925712585449,6.268491744995117,6.0042805671691895,6.283377170562744,6.0973124504089355,6.737371921539307,6.411761283874512,6.763422012329102,6.7113237380981445,6.854593753814697,6.90669059753418,6.9587883949279785,7.100196361541748,7.122524738311768,6.997862815856934,6.748537063598633,6.558751583099365,6.852732181549072,6.977395534515381,6.815519332885742,6.828543663024902,6.839707851409912,6.917853355407715,7.0778703689575195,6.981115818023682,6.930880546569824,6.9494853019714355,6.951345920562744,6.977395534515381,6.982976913452148,6.975534915924072,6.9494853019714355,6.910410404205322,6.936460018157959,6.889945030212402,6.878781795501709,7.195088863372803,7.196950912475586,7.448136806488037,7.442553520202637,7.472324848175049,7.596986293792725,7.563497066497803,7.345800399780273,7.38301420211792,7.642133712768555,7.715361595153809,7.681564807891846,7.720994472503662,7.659032821655273,7.683441638946533,7.76230525970459,7.681564807891846,7.4750213623046875,7.2834978103637695,7.2027587890625,7.076953411102295,7.127649307250977,7.0938520431518555,7.172713279724121,7.204634666442871,7.131405830383301,7.268474578857422,7.508817672729492,7.585803508758545,7.589558124542236,7.585803508758545,7.677809238433838,7.687196731567383,7.446854114532471,7.570781230926514,7.525718688964844,7.555759906768799,7.570781230926514,7.644010543823242,7.563270568847656,7.583925247192383,7.384892463684082,7.236556053161621,7.354849815368652,7.533229351043701,7.5144524574279785,7.347339630126953,7.418690204620361,7.546372413635254,7.465631484985352,7.33231782913208,7.360482215881348,7.354849815368652,7.521964073181152,7.555759906768799,7.568903923034668,7.53698205947876,7.655276298522949,7.6609110832214355,7.544495582580566,7.411179542541504,7.683441638946533,8.150982856750488,8.162247657775879,8.256133079528809,8.209192276000977,8.265521049499512,8.288052558898926,8.14985466003418,8.1214599609375,8.111991882324219,8.140390396118164,8.132818222045898,8.049520492553711,8.047626495361328,8.14606761932373,8.176358222961426,8.157427787780762,8.308877944946289,8.397854804992676,8.433822631835938,8.265335083007812,8.337275505065918,8.09684944152832,8.132818222045898,8.352418899536133,8.246406555175781,8.390279769897461,8.714004516601562,8.65910530090332,8.878704071044922,8.890064239501953,8.96389389038086,8.846521377563477,8.787835121154785,8.941178321838379,8.835163116455078,8.86545467376709,8.886276245117188,8.93549919128418,8.886276245117188,8.611774444580078,8.579593658447266,8.572019577026367,8.683712005615234,8.738614082336426,8.679927825927734,8.50954818725586,8.626920700073242,8.782154083251953,8.585270881652832,8.55119514465332,8.672354698181152,8.655316352844238,8.636384963989258,8.727254867553711,8.98093318939209,8.88817024230957,8.895742416381836,8.793514251708984,8.562554359436035,8.48682975769043,8.132818222045898,8.308877944946289,8.587165832519531,8.746187210083008,8.043842315673828,8.041947364807129,7.795843601226807,7.9151105880737305,7.89617919921875,7.877082347869873,7.98020076751709,7.98020076751709,8.087138175964355,8.169251441955566,8.243721961975098,8.211262702941895,8.398401260375977,8.327747344970703,8.071864128112793,7.96683406829834,7.896178245544434,7.844620227813721,7.8675336837768555,7.829343318939209,7.695671558380127,7.7204976081848145,7.869444847106934,7.7376837730407715,7.924822807312012,8.11196231842041,8.276187896728516,8.295283317565918,8.398401260375977,8.480515480041504,8.390764236450195,8.310561180114746,8.220809936523438,8.38885498046875,8.490062713623047,8.539711952209473,8.612277030944824,8.791779518127441,8.971282005310059,8.660016059875488,8.530162811279297,8.449960708618164,8.698208808898926,8.72876262664795,8.797506332397461,8.818512916564941,8.927359580993652,8.946455955505371,8.963642120361328,8.940727233886719,8.68865966796875,8.77268123626709,8.512979507446289,8.50343132019043,7.099878311157227,7.273651123046875,7.096059799194336,7.220181465148926,7.34430456161499,7.497073173522949,7.181989669799805,7.239277362823486,6.996758460998535,6.876454830169678,6.689313888549805,6.695102214813232,6.534960746765137,6.324652671813965,6.424982070922852,6.380606174468994,6.509877681732178,6.2590532302856445,6.176086902618408,5.788273334503174,5.840367317199707,5.892462253570557,5.89631986618042,5.604977607727051,5.5490241050720215,5.54709529876709,5.518153667449951,5.54709529876709,5.473776817321777,5.493071556091309,5.485353469848633,5.495001316070557,5.410106182098389,5.462200164794922,5.5509538650512695,5.473776817321777,5.4892120361328125,5.473776817321777,5.6686482429504395,5.37923526763916,5.197870254516602,4.935466766357422,4.9470438957214355,4.921961784362793,4.860219955444336,4.879513740539551,4.952832221984863,4.835136890411377,5.028079032897949,5.045444488525391,4.960549354553223,5.057021617889404,5.172786235809326,5.001067638397217,5.0493035316467285,5.2113752365112305,5.176645278930664,5.381165027618408,5.232597827911377,5.141915798187256,5.1457743644714355,5.205586910247803,5.402388572692871,5.545166015625,5.641636848449707,5.439047336578369,5.635848522186279,5.680225372314453,5.767049312591553,5.78055477142334,5.892462253570557,5.9464850425720215,5.969638347625732,6.037168979644775,6.311147212982178,6.094531059265137,5.998907566070557,5.877914905548096,6.1062397956848145,5.940362930297852,6.000858783721924,6.178444862365723,6.006713390350342,6.227232456207275,6.119900226593018,6.016470909118652,6.020373344421387,5.889623165130615,5.926702499389648,5.907186508178711,5.872060775756836,6.149172782897949,6.197959899902344,6.192106246948242,6.115997791290283,6.035985469818115,5.911089897155762,5.872060775756836,5.682764053344727,5.754969596862793,5.831077575683594,5.872060775756836,6.141366481781006,6.176494121551514,6.20381498336792,6.285777568817139,6.332613945007324,6.418478488922119,6.30529260635376,6.40091609954834,6.40091609954834,6.50239372253418,6.514103412628174,6.420431613922119,6.40091609954834,6.3150506019592285,6.108190536499023,5.998907566070557,5.875962257385254,5.872060775756836,5.891574382781982,5.955974578857422,5.698376655578613,5.678861141204834,5.606656074523926,5.6632490158081055,5.5539655685424805,5.470051288604736,5.571528911590576,5.557868480682373,5.555916786193848,5.60080099105835,5.801806449890137,5.850592613220215,5.620316505432129,5.678861141204834,5.649588108062744,5.637879848480225,5.587141513824463,5.628658294677734,5.626681327819824,5.581209659576416,5.39141321182251,5.245111465454102,5.14625883102417,5.086947441101074,5.16602897644043,5.126488208770752,5.169983386993408,5.219409465789795,5.108695030212402,5.140327453613281,5.205570697784424,5.0098419189453125,5.04147481918335,5.15021276473999,5.221386909484863,5.2549967765808105,5.3498945236206055,5.199639320373535,5.233249187469482,5.205570697784424,5.411182880401611,5.624704360961914,5.682039260864258,5.703786849975586,5.658315658569336,5.5337605476379395,5.968710899353027,5.968710899353027,6.1525774002075195,6.130829334259033,6.0912885665893555,6.105127334594727,6.17827844619751,6.1921186447143555,6.16246223449707,6.118967056274414,6.000344753265381,5.7808918952941895,5.859973907470703,5.863926887512207,5.939055919647217,5.889629364013672,5.857996940612793,5.960803985595703,6.150599956512451,6.198049068450928,6.273176670074463,6.16246223449707,6.093265533447266,6.16246223449707,6.271199703216553,6.219796180725098,6.344351291656494,6.269222259521484,6.358189105987549,5.682039260864258,5.727510929107666,5.632613182067871,5.612842082977295,5.5416693687438965,5.612842082977295,5.608888626098633,5.634929656982422,5.564818382263184,5.444628715515137,5.41658353805542,5.4065680503845215,5.414580821990967,5.4586501121521,5.426599502563477,5.5888566970825195,5.552799701690674,5.634929656982422,5.6629743576049805,5.64694881439209,5.536773681640625,5.4947075843811035,5.5067267417907715,5.436615467071533,5.526758670806885,5.564818382263184,5.434611797332764,5.448635578155518,5.3444695472717285,5.3444695472717285,5.37451696395874,5.218269348144531,5.2322916984558105,5.102085590362549,5.084056854248047,4.947841167449951,4.971879005432129,5.007936000823975,5.029971599578857,5.009939670562744,5.035980224609375,4.95785665512085,4.961863994598389,4.805615425109863,4.7875871658325195,4.817634582519531,4.719478607177734,4.192643642425537,4.17261266708374,4.152580261230469,4.25474214553833,4.188637733459473,4.312834739685059,4.380942344665527,4.471086025238037,4.605298042297363,4.537189483642578,4.619319915771484,4.699447154998779,4.699447154998779,4.699447154998779,4.829653263092041,5.220272541046143,5.172196865081787,5.0379838943481445,4.979024410247803,5.019686222076416,5.009520530700684,4.934296607971191,4.985123157501221,5.060348033905029,5.2738213539123535,5.27992057800293,5.290086269378662,5.3714094161987305,5.365310192108154,5.139638423919678,5.151836395263672,5.168101787567139,5.265688419342041,5.310417175292969,5.365310192108154,5.094910144805908,5.1660685539245605,5.275854110717773,5.137604713439941,5.151836395263672,5.135571479797363,5.157936096191406,5.2697553634643555,5.0827107429504395,4.985123157501221,4.979024410247803,5.009520530700684,5.003421783447266,5.025784969329834,4.621201992034912,4.745219707489014,4.775716304779053,4.739120006561279,4.794013500213623,4.865171432495117,4.852973461151123,4.913965702056885,4.924131393432617,4.9424285888671875,4.915998458862305,4.979024410247803,4.940395832061768,4.956660270690918,5.029851913452148,5.017653465270996,5.0074872970581055,5.040017604827881,5.162001132965088,5.21689510345459,5.157936096191406,5.233160495758057,5.241292476654053,5.168101787567139,5.1985979080200195,5.330748081207275,5.33888053894043,5.196564674377441,5.342946529388428,5.391740322113037,4.968859672546387,4.976991653442383,5.0786452293396,5.139638423919678,5.064414024353027,5.015620231628418,5.0827107429504395,5.0827107429504395,5.19832181930542,4.993940353393555,5.0703253746032715,5.093033790588379,5.008391380310059,5.086840629577637,4.929941177368164,4.956779479980469,4.973295211791992,4.9464569091796875,4.273441314697266,4.304408550262451,4.484016418457031,4.53149938583374,4.636786937713623,4.655366897583008,4.54182243347168,4.537693023681641,4.492275714874268,4.508790493011475,4.471630573272705,4.517048358917236,4.564531326293945,4.556272983551025,4.6202712059021,4.725559711456299,4.715236663818359,4.702850818634033,4.7874932289123535,4.7874932289123535,4.793686389923096,4.830846309661865,4.882458209991455,4.768913745880127,4.68427038192749,4.702850818634033,4.839105129241943,4.948521137237549,4.86594295501709,4.954714298248291,5.033164978027344,5.055873394012451,5.150839805603027,5.026971340179443,4.960908889770508,5.029036045074463,5.0517449378967285,4.9216837882995605,4.90929651260376,5.000133037567139,4.965036869049072,4.678077220916748,4.688399314880371,4.876265525817871,4.587240219116211,4.659496307373047,4.5707244873046875,4.702850818634033,4.680140972137451,4.720034599304199,4.598254203796387,4.627650260925293,4.486972808837891,4.6213507652282715,4.558360576629639,4.615051746368408,4.541563034057617,4.455477714538574,4.32319974899292,4.3672919273376465,4.3336968421936035,4.29590368270874,4.312701225280762,4.33579683303833,4.436580657958984,4.489072799682617,4.5163679122924805,4.537364482879639,4.537364482879639,4.53526496887207,4.5163679122924805,4.434481620788574,4.390388488769531,4.386188983917236,4.400886058807373,4.4071855545043945,4.442879676818848,4.413484573364258,4.468075752258301,4.428182125091553,4.482773303985596,4.430281639099121,4.363092422485352,4.3672919273376465,4.463876724243164,4.417684078216553,4.5562615394592285,4.514267921447754,4.55416202545166,4.484873294830322,4.489072799682617,4.547863006591797,4.604553699493408,4.654945373535156,4.606653690338135,4.636047840118408,4.507968902587891,4.568859100341797,4.587756633758545,4.394587993621826,4.491171836853027,4.430281639099121,4.455477714538574,4.405085563659668,4.5436625480651855,4.510068893432617,4.57305908203125,4.073339462280273,4.020848274230957,3.936861991882324,3.945260524749756,3.8843700885772705,3.920064926147461,3.9767556190490723,4.060741424560547,4.037182331085205,4.101434707641602,4.112143516540527,4.182821273803711,4.287766456604004,4.300616264343262,4.345592975616455,4.319891929626465,4.324175834655762,4.304900169372559,4.259923458099365,4.2856245040893555,4.377719879150391,4.422695636749268,4.465530872344971,4.4526801109313965,4.424837589263916,4.3841447830200195,4.3284592628479,4.337026119232178,4.394853115081787,4.287766456604004,4.315608501434326,4.332742691040039,4.195672035217285,4.176395893096924,4.221371650695801,4.157120704650879,4.210663318634033,4.294190883636475,4.294190883636475,4.3113250732421875,4.343451499938965,4.2749152183532715,4.199954986572266,4.178537368774414,4.142127513885498,4.02004861831665,4.002914905548096,3.9836390018463135,3.9643635749816895,3.876552104949951,3.8187248706817627,3.6645195484161377,3.6837949752807617,3.7608978748321533,3.51888108253479,3.469621181488037,3.4674792289733887,3.426786422729492,3.4653375148773193,3.4931797981262207,3.5210230350494385,3.5831332206726074,3.720205068588257,3.7309134006500244,3.891543388366699,4.073591709136963,4.180678367614746,4.095492839813232,4.099862098693848,4.2374701499938965,4.2090744972229,4.152283191680908,4.069281578063965,4.193785190582275,4.165389060974121,4.174126148223877,4.078019142150879,4.014675140380859,4.0059380531311035,4.07583475112915,4.016859531402588,3.9862797260284424,4.029964923858643,3.99501633644104,4.0430707931518555,3.9862797260284424,3.9688055515289307,3.9207520484924316,3.988464117050171,3.975358724594116,4.0015692710876465,4.080203056335449,4.2003374099731445,4.270233631134033,4.298629283905029,4.359788417816162,3.879251003265381,3.748195171356201,3.822460412979126,3.9010934829711914,3.960068702697754,3.833381175994873,3.8006174564361572,3.7088782787323,3.6782987117767334,3.7263529300689697,3.7460110187530518,3.72853684425354,3.671745777130127,3.638981819152832,3.5450587272644043,3.4183712005615234,3.525400400161743,3.5974812507629395,3.457688093185425,3.5319533348083496,3.4511353969573975,3.4030816555023193,3.542874336242676,3.5843753814697266,3.582190990447998,3.464240789413452,3.4271082878112793,3.411818742752075,3.4882681369781494,3.5122945308685303,3.40089750289917,3.4271082878112793,3.4882681369781494,3.564342975616455,3.5911927223205566,3.5934300422668457,3.566580295562744,3.499455213546753,3.546442985534668,3.4793179035186768,3.4927425384521484,3.4591803550720215,3.4256176948547363,3.450230360031128,3.3137428760528564,3.2376675605773926,3.136979818344116,3.0944671630859375,3.020629644393921,3.1414549350738525,3.1056549549102783,3.166067361831665,2.8237290382385254,2.8684794902801514,2.910991668701172,2.9848294258117676,3.034054756164551,3.004967212677002,3.0161542892456055,3.0609047412872314,3.0967047214508057,3.0497171878814697,3.0452418327331543,3.0899922847747803,3.11907958984375,3.056429624557495,3.0251047611236572,2.881904363632202,2.9535045623779297,3.0004920959472656,3.0116796493530273,3.058666944503784,3.101179838180542,3.054192066192627,3.098942518234253,3.00944185256958,2.8707168102264404,2.908754587173462,2.884141683578491,2.861767053604126,2.893091917037964,2.9154670238494873,2.8438668251037598,2.9669296741485596,3.022867202758789,3.0318169593811035,3.0474796295166016,2.7879292964935303,2.8595292568206787,2.834916830062866,2.846104383468628,2.850579261779785,2.834916830062866,2.9199419021606445,3.0027294158935547,2.9535045623779297,3.069854736328125,3.186204671859741,3.2667551040649414,3.2264797687530518,3.2421422004699707,3.2510924339294434,3.2832586765289307,3.228116512298584,3.062689781188965,2.9524056911468506,3.2074379920959473,3.492339611053467,3.6187071800231934,3.6095166206359863,3.568160057067871,3.5658626556396484,3.471660852432251,3.439495086669922,3.3544843196868896,3.418816566467285,3.3475914001464844,3.253389835357666,3.228116512298584,3.361377000808716,3.480851411819458,3.5543744564056396,3.4142212867736816,3.37746000289917,3.4670660495758057,3.5107202529907227,3.4969348907470703,3.349888801574707,3.349888801574707,3.428006887435913,3.464768171310425,3.421114206314087,3.395840644836426,3.333806037902832,3.40273380279541,3.4073286056518555,3.37746000289917,3.3108298778533936,3.384352684020996,3.359079122543335,3.411923885345459,3.4142212867736816,3.473958730697632,3.5038275718688965,3.4946370124816895,3.5199105739593506,3.4946370124816895,3.561267375946045,3.542886734008789,3.4969348907470703,3.5222082138061523,3.6416831016540527,3.788728713989258,3.901310682296753,3.8507637977600098,3.8025143146514893,3.3797576427459717,3.2235212326049805,3.244199752807617,3.1201295852661133,3.0489044189453125,3.228116512298584,3.735884428024292,3.708313226699829,3.7060153484344482,3.6761467456817627,3.7129082679748535,3.8277878761291504,3.9150965213775635,3.857656717300415,3.904672622680664,3.8788137435913086,3.9023218154907227,3.876462936401367,3.8835155963897705,3.6484358310699463,3.7659759521484375,3.664891481399536,3.6554882526397705,3.5896661281585693,3.5920166969299316,3.495634078979492,3.507388114929199,3.483880043029785,3.4509689807891846,3.5214927196502686,3.4697751998901367,3.4862308502197266,3.4462673664093018,3.4791786670684814,3.4979848861694336,3.594367742538452,3.6014199256896973,3.540299415588379,3.4627230167388916,3.5544040203094482,3.5896661281585693,3.542649984359741,3.394549608230591,3.2229416370391846,3.4157071113586426,3.448618173599243,3.4321627616882324,3.6084723472595215,3.669593095779419,3.52384352684021,3.5144405364990234,3.5026862621307373,3.493283271789551,3.441565990447998,3.2629053592681885,3.2629053592681885,3.0466320514678955,3.0865957736968994,3.0066685676574707,3.0630874633789062,2.886777639389038,3.2229416370391846,3.173574924468994,3.4274609088897705,3.46037220954895,3.528545379638672,3.4392151832580566,3.2111878395080566,3.260554552078247,3.173574924468994,3.1876800060272217,3.2158892154693604,3.1989636421203613,3.131260633468628,3.1989636421203613,3.092573404312134,3.0853195190429688,3.0587217807769775,3.0780653953552246,3.0417962074279785,3.0055267810821533,2.8918824195861816,2.8217616081237793,2.998272657394409,2.945077657699585,2.969257116317749,3.0514678955078125,3.160276174545288,3.136096715927124,3.684973955154419,3.7430050373077393,3.822798013687134,3.863903045654297,3.85906720161438,3.8324697017669678,3.7816925048828125,3.7550947666168213,3.7913644313812256,3.8131260871887207,3.851813554763794,3.692228078842163,3.7430050373077393,3.8203799724578857,3.84455943107605,3.7478411197662354,2.727461099624634,2.7081172466278076,2.741968870162964,2.7177891731262207,2.749222755432129,2.8507771492004395,2.783074378967285,2.773402452468872,2.744386911392212,2.732296943664551,2.792746067047119,2.773402452468872,2.739550828933716,2.763730525970459,2.7081172466278076,2.7081172466278076,2.6670119762420654,2.749222755432129,2.792746067047119,2.8145077228546143,2.8217616081237793,2.8290154933929443,2.8411052227020264,2.797581911087036,2.8048360347747803,2.795164108276367,2.8024179935455322,2.6525044441223145,2.722625255584717,2.773402452468872,2.799999952316284,2.737499952316284,2.765000104904175,2.7674999237060547,2.740000009536743,2.625,2.637500047683716,2.612499952316284,2.5350000858306885,2.5875000953674316,2.572499990463257,2.547499895095825,2.5399999618530273,2.5924999713897705,2.5250000953674316,2.4075000286102295,2.507499933242798,2.4649999141693115,2.484999895095825,2.4549999237060547,2.492500066757202,2.440000057220459,2.3299999237060547,2.234999895095825,2.2699999809265137,2.234999895095825,2.192500114440918,2.1624999046325684,2.2225000858306885,2.252500057220459,2.237499952316284,2.2225000858306885,2.190000057220459,2.1624999046325684,2.127500057220459,2.192500114440918,2.242500066757202,2.2125000953674316,2.192500114440918,2.172499895095825,2.130000114440918,2.119999885559082,2.065000057220459,2.132499933242798,2.172499895095825,2.1675000190734863,2.1524999141693115,2.015000104904175,2.0325000286102295,1.975000023841858,1.9249999523162842,1.9550000429153442,1.934999942779541,1.8925000429153442,1.899999976158142,1.8949999809265137,1.8674999475479126,1.9550000429153442,1.2599999904632568,1.2825000286102295,1.2549999952316284,1.3600000143051147,1.4299999475479126,1.375,1.4249999523162842,1.4075000286102295,1.4249999523162842,1.4325000047683716,1.4075000286102295,1.3825000524520874,1.3550000190734863,1.3424999713897705,1.3624999523162842,1.3674999475479126,1.3849999904632568,1.3674999475479126,1.340000033378601,1.3450000286102295,1.3274999856948853,1.3799999952316284,1.3624999523162842,1.3274999856948853,1.2949999570846558,1.2100000381469727,1.2274999618530273,1.1875,1.1575000286102295,1.0950000286102295,1.0499999523162842,1.0800000429153442,1.034999966621399,1.0225000381469727,1.0199999809265137,0.9950000047683716,1.002500057220459,1.0299999713897705,1.0075000524520874,1.0049999952316284,0.9599999785423279,0.9449999928474426,0.9275000095367432,0.9524999856948853,0.9524999856948853,0.9725000262260437,0.8974999785423279,0.8774999976158142,0.8675000071525574,0.8299999833106995,0.8025000095367432,0.8299999833106995,0.8450000286102295,0.8550000190734863,0.8849999904632568,0.9674999713897705,0.9125000238418579,0.9549999833106995,0.925000011920929,0.9700000286102295,1.0575000047683716,0.9925000071525574,0.9524999856948853,0.9950000047683716,1.0575000047683716,1.0774999856948853,1.190000057220459,1.2725000381469727,1.1475000381469727,1.1449999809265137,1.1024999618530273,1.087499976158142,1.0824999809265137,1.149999976158142,1.1100000143051147,1.1749999523162842,1.2549999952316284,1.252500057220459,1.2999999523162842,1.3200000524520874,1.3350000381469727,1.3799999952316284,1.3949999809265137,1.3300000429153442,1.3550000190734863,1.3875000476837158,1.372499942779541,1.3075000047683716,1.247499942779541,1.2625000476837158,1.3424999713897705,1.3949999809265137,1.402500033378601,1.4700000286102295,1.5075000524520874,1.4850000143051147,1.4824999570846558,1.597499966621399,1.6074999570846558,1.6050000190734863,1.587499976158142,1.5475000143051147,1.4524999856948853,1.4325000047683716,1.3600000143051147,1.4600000381469727,1.462499976158142,1.4774999618530273,1.5225000381469727,1.5549999475479126,1.5225000381469727,1.5049999952316284,1.4800000190734863,1.4850000143051147,1.4950000047683716,1.4700000286102295,1.4049999713897705,1.375,1.3650000095367432,1.375,1.4149999618530273,1.5075000524520874,1.524999976158142,1.587499976158142,1.5850000381469727,1.5425000190734863,1.5299999713897705,1.6074999570846558,1.600000023841858,1.6699999570846558,1.5824999809265137,1.627500057220459,1.3825000524520874,1.3949999809265137,1.3624999523162842,1.375,1.5149999856948853,1.5399999618530273,1.5149999856948853,1.497499942779541,1.402500033378601,1.3600000143051147,1.350000023841858,1.475000023841858,1.5325000286102295,1.5199999809265137,1.5774999856948853,1.4700000286102295,1.462499976158142,1.3799999952316284,1.4299999475479126,1.3875000476837158,1.3574999570846558,1.3574999570846558,1.1775000095367432,1.152500033378601,1.1549999713897705,1.1875,1.1475000381469727,1.1399999856948853,1.1549999713897705,1.0800000429153442,1.0700000524520874,1.0525000095367432,1.0325000286102295,0.9825000166893005,0.9599999785423279,0.987500011920929,1.0175000429153442,1.0449999570846558,1.034999966621399,0.9524999856948853,0.9850000143051147,1.0049999952316284,1.0475000143051147,1.027500033378601,1.0049999952316284,1.0149999856948853,1.037500023841858,1.034999966621399,1.0099999904632568,0.925000011920929,0.8899999856948853,0.8475000262260437,0.8675000071525574,0.8999999761581421,0.9574999809265137,0.9075000286102295,0.9424999952316284,0.9900000095367432,0.9800000190734863,0.925000011920929,1.0575000047683716,1.034999966621399,0.9950000047683716,1.1475000381469727,1.0924999713897705,1.0575000047683716,0.9424999952316284,1.0475000143051147,0.9399999976158142,0.9524999856948853,1.0399999618530273,1.0425000190734863,1.1024999618530273,1.0549999475479126,0.9125000238418579,0.875,0.8125,0.7124999761581421,0.699999988079071,0.7724999785423279,0.8174999952316284,0.8525000214576721,0.9725000262260437,1.184999942779541,1.4874999523162842,1.3174999952316284,1.2575000524520874,1.2200000286102295,1.402500033378601,1.1950000524520874,1.222499966621399,1.1749999523162842,1.1924999952316284,1.4550000429153442,1.409999966621399,1.5099999904632568,1.4325000047683716,1.5125000476837158,1.3700000047683716,1.347499966621399,1.2324999570846558,1.2174999713897705,1.2450000047683716,1.190000057220459,1.1349999904632568,1.0525000095367432,1.0325000286102295,1.0549999475479126,1.1449999809265137,1.1100000143051147,1.1074999570846558,1.1100000143051147,1.0449999570846558,1.1050000190734863,1.1725000143051147,1.0824999809265137,1.0149999856948853,1.0325000286102295,1.0449999570846558,1.1100000143051147,1.1174999475479126,1.034999966621399,1.252500057220459,1.2400000095367432,1.2675000429153442,1.0924999713897705,1.1799999475479126,1.1725000143051147,1.159999966621399,1.190000057220459,1.2374999523162842,1.2200000286102295,1.2174999713897705,1.2074999809265137,1.1024999618530273,1.1150000095367432,1.087499976158142,1.0950000286102295,1.0850000381469727,1.1100000143051147,1.0724999904632568,1.059999942779541,1.0225000381469727,1.065000057220459,1.0525000095367432,1.0850000381469727,1.065000057220459,1.0199999809265137,1.0475000143051147,1.0425000190734863,0.9900000095367432,0.9624999761581421,1.002500057220459,1.027500033378601,1.027500033378601,1.0075000524520874,1.002500057220459,0.9850000143051147,1.0149999856948853,1.024999976158142,1.002500057220459,1.037500023841858,1.1074999570846558,1.1575000286102295,1.1074999570846558,1.0399999618530273,1.0824999809265137,1.087499976158142,1.1299999952316284,1.159999966621399,1.1875,1.1575000286102295,1.2024999856948853,1.1799999475479126,1.152500033378601,1.2575000524520874,1.2174999713897705,1.2450000047683716,1.277500033378601,1.3125,1.347499966621399,1.6699999570846558,1.912500023841858,1.9275000095367432,1.9550000429153442,1.912500023841858,1.9249999523162842,1.837499976158142,1.5575000047683716,1.5225000381469727,1.7274999618530273,1.7725000381469727,2.1700000762939453,2.299999952316284,2.367500066757202,2.1875,2.640000104904175,2.509999990463257,2.2850000858306885,2.505000114440918,2.5225000381469727,2.5875000953674316,2.549999952316284,2.442500114440918,2.3475000858306885,2.365000009536743,2.2825000286102295,2.3399999141693115,3.372499942779541,3.005000114440918,2.950000047683716,2.9700000286102295,3.0625,3.4574999809265137,3.327500104904175,3.4774999618530273,3.4649999141693115,3.5250000953674316,3.7274999618530273,3.75,3.362499952316284,3.172499895095825,2.9549999237060547,2.932499885559082,2.617500066757202,2.6875,2.8924999237060547,2.7274999618530273,2.862499952316284,2.9649999141693115,2.872499942779541,2.7750000953674316,2.9375,2.7825000286102295,2.752500057220459,3.015000104904175,2.9075000286102295,2.8924999237060547,3.115000009536743,3.177500009536743,3.4749999046325684,3.4175000190734863,3.6875,4.019999980926514,4.139999866485596,3.950000047683716,4.144999980926514,4.03000020980835,4.224999904632568,4.087500095367432,4.235000133514404,3.4149999618530273,3.5299999713897705,3.327500104904175,3.180000066757202,3.4625000953674316,3.4625000953674316,3.7074999809265137,3.9075000286102295,3.882499933242798,4.864999771118164,5.142499923706055,5.037499904632568,5.247499942779541,4.84499979019165,4.815000057220459,4.710000038146973,4.3125,4.34250020980835,4.590000152587891,4.519999980926514,4.422500133514404,4.985000133514404,4.987500190734863,7.849999904632568,9.977499961853027,8.875,9.84000015258789,9.779999732971191,10.757499694824219,16.252500534057617,19.197500228881836,36.994998931884766,86.87750244140625,48.400001525878906,81.25,56.25,22.5,23.102500915527344,13.375,15.942500114440918,15.0,12.577500343322754,12.800000190734863,12.774999618530273,13.100000381469727,12.3774995803833,11.484999656677246,10.172499656677246,10.147500038146973,11.5,11.242500305175781,22.927499771118164,27.1825008392334,25.434999465942383,30.100000381469727,29.545000076293945,31.045000076293945,33.087501525878906,34.435001373291016,48.625,61.724998474121094,66.25,65.0,66.125,55.03499984741211,52.04249954223633,52.45249938964844,50.4375,50.067501068115234,48.622501373291016,45.4375,30.084999084472656,45.9375,45.25,45.32500076293945,48.6150016784668,47.45500183105469,47.86249923706055,46.73749923706055,46.125,44.49250030517578,42.564998626708984,39.59000015258789,35.272499084472656,35.247501373291016,41.63249969482422,39.11000061035156,38.67250061035156,41.092498779296875,39.63249969482422,39.627498626708984,37.79249954223633,37.79499816894531,42.23249816894531,44.442501068115234,44.64500045776367,44.04750061035156,43.397499084472656,40.54999923706055,40.182498931884766,39.869998931884766,40.252498626708984,40.27750015258789,35.80500030517578,36.72999954223633,36.1974983215332,41.125,39.97999954223633,45.150001525878906,45.16749954223633,42.20750045776367,42.622501373291016,44.1974983215332,45.002498626708984,52.35749816894531,60.63999938964844,63.532501220703125,55.5,62.255001068115234,70.55999755859375,64.54499816894531,62.09000015258789,70.00250244140625,75.0,75.63999938964844,55.09749984741211,58.334999084472656,57.36000061035156],"type":"scatter","xaxis":"x","yaxis":"y"},{"name":"Revenue","x":["2020-01-01T00:00:00","2019-01-01T00:00:00","2018-01-01T00:00:00","2017-01-01T00:00:00","2016-01-01T00:00:00","2015-01-01T00:00:00","2014-01-01T00:00:00","2013-01-01T00:00:00","2012-01-01T00:00:00","2011-01-01T00:00:00","2010-01-01T00:00:00","2009-01-01T00:00:00","2008-01-01T00:00:00","2007-01-01T00:00:00","2006-01-01T00:00:00","2005-01-01T00:00:00"],"y":[6466.0,8285.0,8547.0,7965.0,9364.0,9296.0,9040.0,8887.0,9551.0,9474.0,9078.0,8806.0,7094.0,5319.0,3092.0,1843.0],"type":"scatter","xaxis":"x2","yaxis":"y2"}],                        {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"xaxis":{"anchor":"y","domain":[0.0,1.0],"matches":"x2","showticklabels":false,"title":{"text":"Date"},"rangeslider":{"visible":true}},"yaxis":{"anchor":"x","domain":[0.6499999999999999,0.9999999999999999],"title":{"text":"Price ($US)"}},"xaxis2":{"anchor":"y2","domain":[0.0,1.0],"title":{"text":"Date"}},"yaxis2":{"anchor":"x2","domain":[0.0,0.35],"title":{"text":"Revenue ($US Millions)"}},"annotations":[{"font":{"size":16},"showarrow":false,"text":"Historical Share Price","x":0.5,"xanchor":"center","xref":"paper","y":0.9999999999999999,"yanchor":"bottom","yref":"paper"},{"font":{"size":16},"showarrow":false,"text":"Historical Revenue","x":0.5,"xanchor":"center","xref":"paper","y":0.35,"yanchor":"bottom","yref":"paper"}],"showlegend":false,"height":900,"title":{"text":"GameStop"}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('359c44ce-308d-462b-9035-f806c3eb99ff');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


<h2>About the Authors:</h2> 

<a href="https://www.linkedin.com/in/joseph-s-50398b136/">Joseph Santarcangelo</a> has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.

Azim Hirjani


## Change Log

| Date (YYYY-MM-DD) | Version | Changed By    | Change Description        |
| ----------------- | ------- | ------------- | ------------------------- |
| 2022-02-28        | 1.2     | Lakshmi Holla | Changed the URL of GameStop |
| 2020-11-10        | 1.1     | Malika Singla | Deleted the Optional part |
| 2020-08-27        | 1.0     | Malika Singla | Added lab to GitLab       |

<hr>

## <h3 align="center"> © IBM Corporation 2020. All rights reserved. <h3/>

<p>

