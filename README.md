# js_biBao_mianXiang_duiXiang
js—闭包与面向对象模式(经典例子)


      闭包可以把一些不需要暴露在全局变量封装成 “ 私有变量”。 这里假设一个乘积运算





            var mult=function(){
                var a=1;
                for(var i=0;i<arguments.length;i++){
                  a=a*arguments[i]
                }
                return a

              }     	
              alert(mult(1,2,3))



      mult可以接受number类型参数，并返回参数乘积，但是对于相同的参数来说，
      每一次计算都是一种浪费，我们可以在这里加入缓存机制来提升这个函数性能







              var ache=Object;
              var mult=function(){
                var arrty=Array.prototype.join.call(arguments,',');
                if('arrty' in ache){
                  return ache[arrty];
                }
                var a=1;
                for(var i=0;i<arguments.length;i++){


                  console.log(a*arguments[i])
                  console.log(a)
                  a=a*arguments[i]
                }
                console.log(ache[arrty])
                console.log(a)
                return a
              }
              console.log(mult(1,2,3,4,5))






      来看看这个闭包相关的代码



          var extnt=function(){
              var val=0;
              return {
                fun:function(){
                 val++;
               console.log(val)

                }
               }
             }
            var extnt_s=extnt();
                 extnt_s.fun()    1
                 extnt_s.fun()    2
                 extnt_s.fun()    3



      又或者

          var exnt=function(){
            this.val=0;
          }
           exnt.prototype.exnt1=function(){
               this.val++;
              console.log(this.val)
           }
           var exnt_s=new exnt()
          exnt_s.exnt1()    1
          exnt_s.exnt1()    2
          exnt_s.exnt1()    3


      用闭包实现命令模式

        这是面向对象写法 

                      <button id='btn1'>来了</button>
          <button id="btn2">走了</button>


          var kl={
            kai:function(){
              console.log('老鼠快来')
            },
            guan:function(){
              console.log('老鼠快走')
            }
          }

          var haha=function(laocan){
            this.laocan=laocan;
          }
          haha.prototype.btn1=function(){
            this.laocan.kai()
          }
          haha.prototype.btn2=function(){
            this.laocan.guan()
          }

          function lao_haha(shows){
            document.getElementById('btn1').onclick=function(){
              document.getElementById('btn2').style.color=''
              document.getElementById('btn1').style.color='red'
              shows.btn1()    老鼠快来
            }
            document.getElementById('btn2').onclick=function(){
              document.getElementById('btn1').style.color=''
              document.getElementById('btn2').style.color='red'
              shows.btn2()  老鼠快走
            }
          }

          var sh=new haha(kl)
          lao_haha(sh)

      闭包写法  同上


                 <button id='btn1'>kai</button>
          <button id="btn2">guan </button>
          <script>
            var ku={
              kai:function(){
                console.log("开始")
              },
              guan:function(){
                console.log("结束")
              }
            }
            var opem=function(ku_s){
               var ex_kai=function(){
                return ku_s.kai()
               }
               var ex_guan=function(){
                return ku_s.guan()
               }
               return{
                ex_kai,
                ex_guan
               }
            }
            var fun=function(cnum){
            document.getElementById('btn1').onclick=function(){
              cnum.ex_kai()
            }	
            document.getElementById('btn2').onclick=function(){
              cnum.ex_guan()
            }
            }
            fun(opem(ku)) 




      函数作为参数传递







              var appdiv=function(){
               for(var i=0;i<100;i++){
                var div=document.createElement('div');
                 div.innerHTML=[i]
                 document.body.appendChild(div);
                  div.style.display='none'	

              }
                       }
                      appdiv()
      同上			    
       回调函数
      把 div.style.display='none'逻辑写在appdiv里面显然不合理，这样appdiv函数很难复用，于是把     div.style.display='none'抽取出来，用回调函数的形式appdiv方法  	

                这里把隐藏点的逻辑放在回调函数中，‘委托’ 给appdiv 会执行之前传入的回调函数

            var appdiv=function(cunm){
              for(var i=0;i<100;i++){
                var div=document.createElement('div');
                 div.innerHTML=[i]
                 document.body.appendChild(div);
                 if(typeof cunm==='function'){
                  console.log(div+'-----')
                  cunm(div)

                 }

              }
                       }

            appdiv(function(node){
              console.log(node+'&&&&&')
              node.style.display='none'	
                 })



      Array.prototype.sort接受一个函数作为参数,这个函数里面封装了数组元素排序规则,
      Array.prototype.sort 是用来对数组进行排序的


            var arr=[1,2,56,78,9,0];
            arr.sort(function(a,b){
              return a-b;
            })
                 console.log(arr)    //  [0, 1, 2, 9, 56, 78]



             var arr=[1,2,56,78,9,0];
            arr.sort(function(a,b){
              return b-a;
            })
            console.log(arr)    //[78, 56, 9, 2, 1, 0]
























































