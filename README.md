# Rocket Assets Fairing

`rocket-assets-fairing` is a Fairing for [Rocket](https://rocket.rs) for easily serving static assets from a folder, with a nice cache policy.

## Installing

Add to your `Cargo.toml`:
```
rocket-assets-fairing = "0.1"
```

## Usage

```rust
use assets_rocket_fairing::{Asset, Assets};

#[rocket::main]
async fn main() {
   rocket::build()
       .attach(Assets::fairing())
       .mount("/assets", routes![style])
       .launch()
       .await;
}

#[get("/style.css")]
async fn style(assets: &Assets) -> Option<Asset> {
   assets.open("style.css").await.ok()
}
```

## Configuration

This is configurable the same way as Rocket.

Either through `Rocket.toml`:
```toml
[default]
assets_dir = "assets"
assets_max_age = 86400
```

Or using environment variables:
- `ROCKET_ASSETS_DIR`
- `ROCKET_ASSETS_MAX_AGE`
