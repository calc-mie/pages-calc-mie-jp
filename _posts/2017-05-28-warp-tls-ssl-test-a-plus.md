---
layout: post
title: "warp-tlsでSSL Testの評価をA+にする"
author: "mkdagjp"
---
[warp-tls](https://hackage.haskell.org/package/warp-tls)でそのままwebサーバを立てると[SSL Server Test](https://www.ssllabs.com/ssltest/)で評価がAとなる．  
評価をA+にするにはHTTPヘッダに[HSTS(HTTP Strict Transport Security)](https://ja.wikipedia.org/wiki/HTTP_Strict_Transport_Security)を追加すればいい．

## コード
```Haskell
{-# LANGUAGE OverloadedStrings #-}
module Lib
  ( runService
  ) where

-- wai
import Network.Wai
  ( Application
  , responseLBS
  )

-- http-types
import Network.HTTP.Types
  ( status200
  , hContentType
  , Header
  , ResponseHeaders
  )

-- warp
import Network.Wai.Handler.Warp
  ( setServerName
  , setPort
  , defaultSettings
  , Settings
  , runSettings
  , Port
  )

-- warp-tls
import Network.Wai.Handler.WarpTLS
  ( tlsSettingsChain
  , runTLS
  , defaultTlsSettings
  )

-- base
import Control.Concurrent(forkIO)

hstsHeader :: Header
hstsHeader = (s, t)
  where s = "Strict-Transport-Security"
        t = "max-age=63072000; includeSubdomains; preload"

htmlHeaders :: ResponseHeaders
htmlHeaders = [ (hContentType, "text/html"), hstsHeader ]

app :: Application
app req f = f $ responseLBS status200 htmlHeaders s
  where s = "<!DOCTYPE html>\n<html><body>Hello, world</body></html>"

settings :: Port -> Settings
settings port = setServerName "Warp" $ setPort port defaultSettings

runService :: IO ()
runService = do
  forkIO $ runSettings (settings 80) app
  runTLS tlsSettings'' (settings 443) app
  where tlsSettings'' = tlsSettingsChain cert chain privkey
        cert    = "/etc/letsencrypt/live/example.com/cert.pem"
        chain   = ["/etc/letsencrypt/live/example.com/chain.pem"]
        privkey = "/etc/letsencrypt/live/example.com/privkey.pem"
```

## 解説
HSTSヘッダとして```hstsHeader```を書いた．  
```responseLBS```で指定するヘッダに追加することでHSTSヘッダを送るようにしている．

## 参考文献
* wai
    * <https://hackage.haskell.org/package/wai>
    * <https://hackage.haskell.org/package/wai-3.2.1.1/docs/Network-Wai.html>
* warp
    * <https://hackage.haskell.org/package/warp>
    * <https://hackage.haskell.org/package/warp-3.2.12/docs/Network-Wai-Handler-Warp.html>
* warp-tls
    * <https://hackage.haskell.org/package/warp-tls>
    * <https://hackage.haskell.org/package/warp-tls-3.2.3/docs/Network-Wai-Handler-WarpTLS.html>
* HSTS
    * <https://ja.wikipedia.org/wiki/HTTP_Strict_Transport_Security>
    * <https://wiki.archlinuxjp.org/index.php/Nginx>
        * HSTSヘッダの設定に関して
