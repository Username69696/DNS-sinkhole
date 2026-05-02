import random
import time
from http.server import BaseHTTPRequestHandler, HTTPServer
import os

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        mode = random.choice(["ok_html", "service_unavailable", "slow_response"])

        if mode == "slow_response":
            time.sleep(random.uniform(1.0, 4.0))
            self.send_response(200)
            self.end_headers()
            self.wfile.write(b"<html><body></body></html>")

        elif mode == "service_unavailable":
            self.send_response(503)
            self.send_header("Retry-After", "30")
            self.end_headers()
            self.wfile.write(b"Service Unavailable")

        elif mode == "ok_html":
            self.send_response(200)
            self.send_header("Content-Type", "text/html")
            self.end_headers()
            self.wfile.write(b"<html><head><title></title></head><body></body></html>")

    def do_HEAD(self):
        self.send_response(200)
        self.end_headers()

    def log_message(self, format, *args):
        return

PORT = int(os.environ.get("PORT", 8080))
HTTPServer.allow_reuse_address = True
print(f"Listening on 0.0.0.0:{PORT}", flush=True)
server = HTTPServer(("0.0.0.0", PORT), Handler)
server.serve_forever()
