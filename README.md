# test6
Page split, previous&amp;next to show different items, each page showed certain items
//simulate browser content display when surfing, previous & next button to control page displayed, each page show certain items

 <style>
        <!--monospace 字体为等宽字体-->
        *{text-decoration:none;font-family:monospace,Times;}
        ul li{list-style-type:none;float:left;width:60px;}
        ul li a{display:inline-block;width:100%;text-align:center;}
        ul li a:hover{background-color:gray;}
    </style>
    <script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
    <script type="text/javascript">
        var curPage = 0;
        var itemLimit = 3;
        $(function(){
            $(".pre").click(function(){
                $.ajax({
                    url:"dataSource.json",
                    type:"GET",
                    dataType: "json",
                    success: function(res){
                            curPage--;
                            if(curPage<=0){
                                curPage =0;
                            }
                        curPage = curPage<= 0 ? 0 : curPage;
                        $(".contxt").empty();
                            for(var i=0;i<3;i++){
                                $(".contxt").append("<span style='display:inline-block;width:400px;'>"+res[curPage*itemLimit+i].title+"</span>");
                                $(".contxt").append("<span style='display:inline-block;width:100px;'>"+res[curPage*itemLimit+i].author+"</span>");
                                $(".contxt").append("<span style='display:inline-block;width:150px;'>"+res[curPage*itemLimit+i].date+"</span>");
                                $(".contxt").append("</br>");
                            }
                    }
                });
            });
            $(".nxt").click(function(){
                $.ajax({
                    url:"dataSource.json",
                    type:"GET",
                    dataType: "json",
                    success: function(res){
                        curPage++;
                        curPage = curPage>= Math.floor(res.length/itemLimit) ? Math.floor(res.length/itemLimit) : curPage;
                        $(".contxt").empty();
                        for(var i=0;i<3;i++){
                            $(".contxt").append("<span style='display:inline-block;width:400px;'>"+res[curPage*itemLimit+i].title+"</span>");
                            $(".contxt").append("<span style='display:inline-block;width:100px;'>"+res[curPage*itemLimit+i].author+"</span>");
                            $(".contxt").append("<span style='display:inline-block;width:150px;'>"+res[curPage*itemLimit+i].date+"</span>");
                            $(".contxt").append("</br>");
                        }
                    }
                });
            });
        })
    </script>
