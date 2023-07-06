git clone https://github.com/AleoHQ/leo
cd leo
cargo install --path .
git clone https://github.com/AleoHQ/snarkOS.git
cd snarkOS
git checkout 3e403cff07f36873a756b9e90d0ab4d7b3b8e969
git switch -c snarkos-old
cargo install --path .
snarkos`
cd $HOME

mkdir demo_deploy_Leo_app && cd demo_deploy_Leo_app

WALLETADDRESS=""

APPNAME=helloworld_"${WALLETADDRESS:4:6}"

leo new "${APPNAME}"

PATHTOAPP=$(realpath -q $APPNAME)

cd $PATHTOAPP && cd ..

PRIVATEKEY=""

RECORD=""

snarkos developer deploy "${APPNAME}.aleo" --private-key "${PRIVATEKEY}" --query "https://vm.aleo.org/api" --path "./${APPNAME}/build/" --broadcast "https://vm.aleo.org/api/testnet3/transaction/broadcast" --fee 600000 --record "${RECORD}"

