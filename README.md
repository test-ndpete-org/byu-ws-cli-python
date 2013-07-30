byu-ws-cli-python
=================

A command-line web service client for calling BYU REST web services.

It handles the authentication work so you don't have to.

To install the code run:

  python setup.py install # use sudo if on unix and wanting to install it system-wide

To create an rpm to install run:

  python setup.py bdist_rpm

Once installed you can run the following script to call web services.

  call_web_service.py

This page will describe the byu_ws_sdk python package.  It contains a command-line script that will allow you to call OIT web services that use the OIT java framework authentication.

It supports URLEncoding and Nonce Encoding.  It also supports WSSession and API Keys.  You can mix and match the encoding and the key type as well.

Installation
Install python 2.7. 
On a *nix machine which doesn't have python pre-installed I recommend installing the source distribution of python2.7 from http://www.python.org/download/
If you want to and have root access to install it system-wide do the following.
tar xvf Python-2.7.3.tar.bz2
cd (Python directory created)
./configure
make
sudo make altinstall # this will install it as /usr/local/bin/python2.7 and it will not interfere with your existing python install that came with the OS
If you want to install it just for your user do the following
tar xvf Python-2.7.3.tar.bz2
cd (Python directory created)
#pick a directory you have access to, to install python on, i.e., for me one could be /home/paul/apps/python273 
./configure --prefix=/home/paul/apps/python273
make
make install # notice that it doesn't require root access.  In this example your python will be in /home/paul/apps/python273/bin/python2.7
#add the python bin directory to your PATH variable.  The following will work for bash
echo '\nexport PATH=$PATH:/home/paul/apps/python273/bin' >> ~/.bash_profile && source ~/.bash_profile
On Mac OS X download and install the python 2.7.3 package from http://www.python.org/download/
On Windows I recommend installing the python 2.7 msi file from http://www.activestate.com/activepython/downloads because it comes pre-bundled with some nice things that help on windows.
Install the needed python modules (Add sudo to each command below if you installed python system-wide)
Setup easy_install if you didn't install the activestate python (everyone not on windows)
wget "http://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz#md5=7df2a529a074f613b509fb44feefe74e"
cd setuptools-0.6c11/
\[sudo\] python2.7 setup.py install
Find out where the scripts directory of your python install is and put is in your PATH variable (ask Paul Eden if you don't know how, it's system dependent).
\[sudo\] easy_install-2.7 simplejson
\[sudo\] easy_install-2.7 requests
\[sudo\] easy_install-2.7 decorator
Check out the source code.
cd to the directory where you want to check out the code
svn co https://source.byu.edu/repo/gaa/byu_ws_sdk/trunk/ oit_web_service_client
Create your credentials file. (credentials.cgi)
If you use API keys you need to specify your api key (private key) and shared secret (public key)
If you use WSSession keys you need to specifiy the netId username and password to use
Both of these are put into the credentials.cgi file.
credentials.py

# this file doesn't go into source control
 
# safeguard this file because if someone else got it they could impersonate you when calling the web services
key = '' 
shared_secret = ''
username = ''
password = ''
Place the file into one of the directories in your python path.  To find out what directories are on the python path do the following:
$ python2.7
Python 2.7.3 (default, Apr 20 2012, 22:39:59) 
[GCC 4.6.3] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
Usage
Calling web services
$ python2.7 call_byu_ws.py -h
Usage: call_byu_ws.py [options] url_to_call
basic script to call a web service passed in.
 
Options:
  -h, --help            show this help message and exit
  -m HTTP_METHOD, --http-method=HTTP_METHOD
                        one of 'GET', 'PUT', 'POST', 'DELETE'
  -b BODY, --body=BODY  filename containing the body for the http request.
  -e ENCODING_TYPE, --encoding-type=ENCODING_TYPE
                        one of URL or Nonce [URL]
  -k KEY_TYPE, --key-type=KEY_TYPE
                        one of API or WsSession [API]
  -a ACTOR, --actor=ACTOR
                        the actor to proxy for
  -c CONTENT_TYPE, --content-type=CONTENT_TYPE
                        the content-type of the http request
  -d, --demo            show the http request and response (like in a demo)

