# smc_coin
Exercise Sui Move Coin (SMC) - First Movers
//smc_coin.move
module smc_coin::smc_coin {
    use sui::object::{UID, new};
    use sui::tx_context::{TxContext, sender};
    use sui::transfer::transfer;
    use std::string::String;

    public struct SMC has key {
        id: UID,
        name: String,
        symbol: String,
        description: String,
        decimals: u8,
    }

    public fun mint(ctx: &mut TxContext) {
        let token = SMC {
            id: new(ctx),
            name: std::string::utf8(b"Sui Move Coin"),
            symbol: std::string::utf8(b"SMC"),
            description: std::string::utf8(b"my name OlympusXVN"),
            decimals: 6,
        };
        transfer(token, sender(ctx));
    }
}

move.toml
[package]
name = "smc_coin"
edition = "2024.beta"

[dependencies]
Sui = { git = "https://github.com/MystenLabs/sui", subdir = "crates/sui-framework/packages/sui-framework", rev = "main" }

[addresses]
smc_coin = "0x0"
