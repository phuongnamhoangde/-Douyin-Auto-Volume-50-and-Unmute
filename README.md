// ==UserScript==
// @name         Douyin Auto Volume 50% and Unmute
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Tự động mở âm thanh video trên Douyin khi vào trang lần đầu và đặt âm lượng 50%.
// @author       Phan Đức
// @match        https://*.douyin.com/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Biến lưu trạng thái mute của người dùng
    let userMuted = false;

    // Hàm mở âm thanh và đặt âm lượng nếu người dùng không tắt âm thanh
    function unmuteAndSetVolume(video, volume) {
        if (!userMuted) {
            video.volume = volume;
            video.muted = false;
        }
    }

    // Hàm kiểm tra và thiết lập âm lượng cho tất cả video
    function initializeVideoSettings() {
        let videos = document.querySelectorAll('video');
        videos.forEach(video => {
            // Mở âm thanh và đặt âm lượng khi trang mới tải
            video.muted = false;
            video.volume = 0.5;

            // Lắng nghe sự thay đổi âm thanh để kiểm tra nếu người dùng tắt âm thanh
            video.onvolumechange = () => {
                if (video.muted) {
                    userMuted = true;
                } else {
                    userMuted = false;
                }
            };
        });
    }

    // Chạy hàm thiết lập ngay khi trang tải
    window.addEventListener('load', initializeVideoSettings);

})();
