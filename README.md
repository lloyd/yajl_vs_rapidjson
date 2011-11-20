A quick and dirty comparison of rapidjson vs yajl for pretty printing
of JSON.

compiling rapidjson:

    $ cd rapidjson/examples/pretty
    $ g++ -O3 -o pretty -I rapidjson/include rapidjson/example/pretty/pretty.cpp

just get json_reformat from the yajl package from your package management
system.

Comparison of pretty printing for test_file.json:

    [lth@lloydpro rapidjson_vs_yajl]$ time json_reformat < test_file.json  > /dev/null
    real          0m0.119s
    user          0m0.113s
    sys           0m0.004s
    [lth@lloydpro rapidjson_vs_yajl]$ time ./pretty < test_file.json  > /dev/null
    real          0m0.175s
    user          0m0.168s
    sys           0m0.005s
    [lth@lloydpro rapidjson_vs_yajl]$ time cat < test_file.json > /dev/null
    real          0m0.006s
    user          0m0.001s
    sys           0m0.005s

Comparison of pretty printing for test_file2.json:

    [lth@lloydpro rapidjson_vs_yajl]$ time ./pretty < test_file2.json  > /dev/null
    real          0m0.119s
    user          0m0.113s
    sys           0m0.005s
    [lth@lloydpro rapidjson_vs_yajl]$ time json_reformat < test_file2.json  > /dev/null
    real          0m0.105s
    user          0m0.099s
    sys           0m0.004s
    [lth@lloydpro rapidjson_vs_yajl]$ time cat < test_file2.json > /dev/null
    real          0m0.006s
    user          0m0.001s
    sys           0m0.004s

Conclusion:

For pretty printing, on osx 10.7, for these two data files, YAJL is 31% faster than
rapidjson.

math: `(/ (+ (- (/ 113 99.0) 1) (- (/ 168 113.0) 1)) 2.0)`

Oh. and `cat` is a couple orders of magnitude faster than either.

