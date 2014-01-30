Python 2.x と Python 3.x を併用するのしんどい  

setuptools を入れるのまではいいけど pip を別々に入れるのができない  

distribute が setuptools にマージされたのはすごい良いと思う -> [hatenablog](http://methane.hatenablog.jp/entry/2013/06/04/distribute_%E3%81%A8_setuptools_%E3%81%8C%E3%83%9E%E3%83%BC%E3%82%B8%E3%81%95%E3%82%8C%E3%81%9F)  

easy_install のためだけに distribute いれて pip のためだけに easy_install いれるのとか狂気でしかないしめちゃくちゃ難しかった  

結局 Homebrew でインストールして virtualenv とかで環境つくるのが無難っぽい -> [qiita](http://qiita.com/redtree/items/3927e042b2ca18f03b8c)  
自分でディレクトリを指定したいときとかどうすればよいかわからない 

IT 全般的に 簡単ですやってみましょう！！ というのは全然簡単じゃないことが多々ある   

Python 3.4 では pyenv で ensurepip までインストールされるっぽいし低能な生命体はそれを待つべきっぽい -> [Python 3.4](http://pelican.aodag.jp/python34noensurepipsoretopyvenvnogeng-xin.html)  

Python 3 は色々かわってるので理由とか探るとなるほどってなる -> [diveintopython3-ja](http://diveintopython3-ja.rdy.jp/porting-code-to-python-3-with-2to3.html)

`xrange() -> range()`  

とかいいなって思うけどリストがほしいときいちいち `list()` するのとかどうなのかなって思う -> [dictview](http://docs.python.jp/3.3/library/stdtypes.html?highlight=view#dictionary-view-objects)  
メモリの節約がシビアに問われるところでは便利なんだろうなという気はするけど 簡単ではなくなったと思う  
2.x と 3.x で混乱しているだけかもしれない  

Windows だと py.exe が付いてて楽しい  
シバンつかえるのも良いと思う -> [py.exe shebang](http://dogwood.skr.jp/blog/2013/12/426/#xampp-cgi)