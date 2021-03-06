.PHONY: default build clean test
SPECS := $(shell find spec -name '*.spec.ts')


default: clean build test

build:
	@./node_modules/.bin/tsc --project tsconfig.json --module es2015 --outDir build/es2015;
	@echo "es6 done"
	@./node_modules/.bin/tsc --project tsconfig.json --module commonjs --outDir build/commonjs \
		--declaration --declarationMap --declarationDir build/types;
	@echo "cjs done"

clean:
	@find build \( -name '*.js' -or -name '*.map' -or -name '*.ts' \) -delete;
	@find build -type d ! -path build -delete
	@echo "'${@}' done"

test: test-node test-browser

test-node: $(SPECS)
	@echo "'${@}' ..."
	@./node_modules/.bin/ts-node \
		--project tsconfig.test.json \
		--require tsconfig-paths/register \
		./node_modules/.bin/jasmine --helper="spec/support/reporter.ts" \
		$^

test-browser:
	@echo "'${@}' ..."
	@./node_modules/.bin/karma start karma.conf.js

watch-test-node:
	fswatch -o src | xargs -n1 -I{} make test-node

bootstrap:
	protoc \
		--ts_out=src \
		--plugin=../bin/protoc-gen-ts \
		--proto_path=src/ \
		--experimental_allow_proto3_optional \
		src/google/protobuf/descriptor.proto \
		src/google/protobuf/compiler/plugin.proto
