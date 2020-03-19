# certmagic-storage-badger

Package storage implements a [certmagic.Storage](https://pkg.go.dev/github.com/caddyserver/certmagic?tab=doc#Storage) on top of a [Badger](https://github.com/dgraph-io/badger) database.

It's an alternative to the default file-system storage used by [CertMagic](https://github.com/caddyserver/certmagic).

# Install

    go get oya.to/certmagic-storage-badger

# Usage

    package main

    import (
    	"github.com/caddyserver/certmagic"
    	"github.com/dgraph-io/badger/v2"
    	"log"
    	storage "oya.to/certmagic-storage-badger"
    )

    func main() {
    	// setup the badger DB
    	db, err := badger.Open(badger.DefaultOptions("").WithInMemory(true))
    	if err != nil {
    		log.Fatalf("Cannot open badger memory DB: %s", err)
    	}

    	// set the default CertMagic storage to replace the file-system based on.
    	certmagic.Default.Storage = storage.New(db)

    	// setup the rest of your CertMagic stuff...
    }
