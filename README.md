# Isohttpd

A lightweight http server that runs in an isolate

   ```dart
   import 'dart:io';
   import 'package:isohttpd/isohttpd.dart';

   Future<HttpResponse> handler(HttpRequest request, IsoLogger log) async {
     var response = jsonResponse(request, {"response": "ok"});
     return response;
   }

   void main() async {
     // set routes
     IsoRoute onGet = IsoRoute(path: "*", handler: handler);
     List<IsoRoute> routes = <IsoRoute>[onGet];
     final router = IsoRouter(routes);

     // run
     IsoHttpdRunner iso = IsoHttpdRunner(host: "localhost", router: router);
     await iso.run(verbose: true);

     // listen to logs
     iso.logs.listen((dynamic data) => print("$data"));
     iso.requestLogs.listen((dynamic data) => print("REQUEST $data"));
     // idle
     while (true) {}
   }
   ```