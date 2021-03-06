# This project is really old and unmaintained. It's kept here for legacy reasons.

We advice you to use this one instead : https://github.com/yolk/valvat

## Description

Use this plugin to validate VAT numbers for european countries.

This plugin is Rails 2.x-only, if you want the same functionnality for Rails 3,
use my : vat_validator available at http://github.com/aurels/vat_validator

## Usage

To validate a model field as a valid intracom VAT number :

  validates_vat_number :vat_number

It may be optional like this :

  validates_vat_number :vat_number, :allow_blank => true

If you want the VAT number's country to match another kind of country field, use
the option :

  validates_vat_number :vat_number, :country_method => :my_method

where it is supposed that your model has a method named 'my_method' which
returns the country code you want to match. The available country codes
available for Europa are: DE, AT, BE, BG, CY, DK, ES, EE, FI, FR, EL, HU, IE,
IT, LV, LT, LU, MT, NL, PL, PT, GB, RO, SK, SI, SE and CZ.

Example :

  class Invoice < ActiveRecord::Base
    validates_vat_number :vat_number, :country_method => :country_code

    # Logic to return the country code
    def country_code
      case country.downcase
        when 'belgium' then 'BE'
        when 'france'  then 'FR'
        when 'sweden'  then 'SE'
  	    # ...
        else nil
      end
    end
  end

## Installation

As a gem in your environment.rb :

  config.gem 'validates_vat_number'

As an old-school Rails plugin :

  script/plugin install git://github.com/aurels/validates_vat_number.git

## Tests

If you want to run the specs :

  rake spec

## Credits

This plugin in released under MIT license by Aurélien Malisart (see LICENSE
file).

(c) http://aurelien.malisart.be
