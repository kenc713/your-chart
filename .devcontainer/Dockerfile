# ==================== Development Stage ====================
FROM node:20-alpine AS development

WORKDIR /app

# git をインストール（git 操作が必要な場合）
RUN apk add --no-cache git

# 依存関係ファイルをコピー
COPY package*.json ./

# 依存関係をインストール
RUN npm ci

# ソースコードをコピー
COPY . .

# セキュリティ: 非root ユーザーを作成して切り替え
RUN addgroup -g 1000 appuser && \
    adduser -D -u 1000 -G appuser appuser && \
    chown -R appuser:appuser /app

USER appuser

# Vite 開発サーバーのポート公開
EXPOSE 5173

# 開発サーバー起動
CMD ["npm", "run", "dev", "--", "--host"]
