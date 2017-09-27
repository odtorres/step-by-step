
npm install enclose -g --registry http://npm.prod.uci.cu/nexus/content/groups/npm/

## mostrar dir de los paquetes
npm root -g

## listar ultimas versiones
npm view npm dist-tags.latest

## veriones que tengo
npm list -g


// open npm

export HTTP_PROXY=http://localhost:6666
export HTTPS_PROXY=http://localhost:6666
export http_proxy=http://localhost:6666
export https_proxy=http://localhost:6666

npm config set registry http://registry.npmjs.org/
npm config set proxy 'http://localhost:6666'
npm config set https-proxy 'http://localhost:6666'
npm config set http-proxy 'http://localhost:6666'

git config --global http.proxy http://localhost:6666
git config --global https.proxy http://localhost:6666
git config --global url."http://".insteadOf git://

git config http.proxy http://localhost:6666
git config https.proxy http://localhost:6666
git config url."http://".insteadOf git://

// close

unset HTTP_PROXY
unset HTTPS_PROXY
unset http_proxy
unset https_proxy

#npm config set registry http://maven.prod.uci.cu:8083
npm config set registry http://npm.prod.uci.cu/nexus/content/groups/npm/
#npm adduser –registry http://npm.prod.uci.cu:8083
npm config delete proxy
npm config delete https-proxy
npm config delete http-proxy

git config –-global –-unset http.proxy
git config –-global –-unset https.proxy
git config –-global –-unset url."http://".insteadOf

git config --unset http.proxy
git config --unset https.proxy
git config --unset url."http://".insteadOf

//get list 
git config --global -l 

## Error: Cannot find module './build/bindings/encode.node' at
cd node_modules/iltorb && npm i && cd ../..