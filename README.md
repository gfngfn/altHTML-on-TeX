# altHTML on TeX

## 概要

(La)TeXマクロを用いて，(La)TeXソースコードからHTMLソースを生成するパッケージです．
ただし現状では空白がろくに扱えず和文にしか使用できません……．

## 使用法

`\newtag`コマンドによりHTMLタグへの変換マクロを登録することができます．
例えば`\hoge{`_内容_`}`で`<div class='hoge'>`_内容_`</div>`を表す`\hoge`を使いたいならば，

    \newtag\hoge{<div class='hoge'>}{</div>}

をプリアンブルに記述しておくと使えるようになります．

## 使用例

今のところ，パッケージを読み込んだ段階では

    \newtag\htmlja{<html lang='ja'>}{</html>}
    \newtag\head{<head>}{</head>}
    \newtag\body{<body>}{</body>}
    \newtag\div{<div>}{</div>}
    \newtag\span{<span>}{</span>}
    \newtag\parag{<p>}{</p>}
    \newtag\imgsrc{<img src="}{" />}
    \newtag\hi{<h1>}{</h1>}
    \newtag\hii{<h2>}{</h2>}
    \newtag\hiii{<h3>}{</h3>}

が登録されているようになっています．これをもとにコマンド`\writehtml{`_出力ファイル名_`}{`_内容_`}`を用いて

    \documentclass{standalone}
    \makeatletter
      \usepackage{althtml-on-tex}
      \def\pair#1#2{［#1・#2］}
    \makeatother
    \begin{document}
      \writehtml{sample.html}{
        \htmlja{
          \head{
          }
          \body{
            \hi{章の例}
            \parag{
              これは段落の例です．
              普通のマクロは全体を括弧で括って使います：{\pair{甲}{子}}
            }
          }
        }
      }
    \end{document}

などと書くことができ，これをpLaTeXでコンパイルすると


    <html lang='ja'>
      
      <head>
        
      </head>
      
      <body>
        
        <h1>
          章の例
        </h1>
        
        <p>
          これは段落の例です．普通のマクロは全体を括弧で括って使います：［甲・子］
        </p>
        
      </body>
      
    </html>
    

と記述された`sample.html`が出力されます．